# SOLID Principles in Python

| Letter | Principle | meaning |
|---|---|---|
| **S** | Single Responsibility Principle | A class should have only one reason to change |
| **O** | Open/Closed Principle | Open for extension, closed for modification |
| **L** | Liskov Substitution Principle | Subclasses must be usable in place of their base class without breaking behavior |
| **I** | Interface Segregation Principle | Don't force classes to implement methods they don't need |
| **D** | Dependency Inversion Principle | Depend on abstractions, not concrete implementations |

# S — Single Responsibility Principle (SRP)

**Definition:** A class should have **one, and only one, reason to change**. It should do one job.

### Violation: `PaymentProcessor` doing everything

```python
class PaymentProcessor:
    def process_payment(self, amount, card_number):
        # 1. Validate card
        if len(card_number) != 16:
            raise ValueError("Invalid card number")

        # 2. Charge the card
        print(f"Charging ${amount} to card {card_number}")

        # 3. Log the transaction
        with open("transactions.log", "a") as f:
            f.write(f"Charged ${amount} to {card_number}\n")

        # 4. Send email receipt
        print(f"Sending email: Your payment of ${amount} was successful")
```

**Problem:** This class has **4 reasons to change**:
1. Card validation rules change
2. Charging logic/payment gateway changes
3. Logging format/storage changes
4. Email/notification provider changes

If the marketing team wants to change the email template, you're editing the same class that processes money. That's a red flag.

### Fix: Split responsibilities into separate classes

```python
class CardValidator:
    def validate(self, card_number):
        if len(card_number) != 16:
            raise ValueError("Invalid card number")
        return True


class PaymentGateway:
    def charge(self, amount, card_number):
        print(f"Charging ${amount} to card {card_number}")
        return {"status": "success", "amount": amount}


class TransactionLogger:
    def log(self, amount, card_number):
        with open("transactions.log", "a") as f:
            f.write(f"Charged ${amount} to {card_number}\n")


class EmailNotifier:
    def send_receipt(self, amount, email):
        print(f"Sending email to {email}: Your payment of ${amount} was successful")


class PaymentProcessor:
    """Now ONLY responsible for orchestrating the payment flow."""
    def __init__(self, validator, gateway, logger, notifier):
        self.validator = validator
        self.gateway = gateway
        self.logger = logger
        self.notifier = notifier

    def process_payment(self, amount, card_number, email):
        self.validator.validate(card_number)
        result = self.gateway.charge(amount, card_number)
        self.logger.log(amount, card_number)
        self.notifier.send_receipt(amount, email)
        return result


# Usage
processor = PaymentProcessor(
    CardValidator(), PaymentGateway(), TransactionLogger(), EmailNotifier()
)
processor.process_payment(100, "1234567812345678", "user@example.com")
```

**Why better:** Each class has exactly one reason to change. Changing the email template only touches `EmailNotifier`. Testing is easier — you can unit-test `CardValidator` in isolation.

---


# O — Open/Closed Principle (OCP)

**Definition:** Classes should be **open for extension but closed for modification**. Add new behavior without editing existing, tested code.

### Violation: `if/elif` chain that must be edited for every new payment method

```python
class PaymentGateway:
    def charge(self, amount, method):
        if method == "credit_card":
            print(f"Charging ${amount} via Credit Card")
        elif method == "paypal":
            print(f"Charging ${amount} via PayPal")
        elif method == "upi":
            print(f"Charging ${amount} via UPI")
        # Every new payment method requires editing this class again!
        else:
            raise ValueError("Unsupported payment method")
```

**Problem:** Adding "Google Pay" means opening this already-tested class and modifying it — risk of breaking existing, working payment methods. Violates OCP.


### Fix: Use abstraction + polymorphism, extend via new classes

```python
from abc import ABC, abstractmethod

class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount):
        ...

class CreditCardPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via Credit Card")

class PayPalPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via PayPal")

class UPIPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via UPI")

# NEW payment method added WITHOUT touching any existing class
class GooglePayPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via Google Pay")


class PaymentGateway:
    """Closed for modification — never needs to change again."""
    def charge(self, amount, method: PaymentMethod):
        method.pay(amount)


# Usage
gateway = PaymentGateway()
gateway.charge(100, CreditCardPayment())
gateway.charge(50, GooglePayPayment())   # extended, zero edits to PaymentGateway
```

**Why better:** `PaymentGateway` never changes again. New payment types are added by **creating new classes**, not editing old ones — reduces regression risk in a system that's already live and tested.



# L — Liskov Substitution Principle (LSP)

**Definition:** Objects of a subclass should be **substitutable for objects of the parent class** without breaking the program. If `B` is a subtype of `A`, you should be able to replace `A` with `B` anywhere without altering correctness.

### Violation: A subclass that breaks the parent's contract

```python
class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount):
        ...

    @abstractmethod
    def refund(self, amount):
        ...

class CreditCardPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via Credit Card")

    def refund(self, amount):
        print(f"Refunding ${amount} to Credit Card")

class GiftCardPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via Gift Card")

    def refund(self, amount):
        # Gift cards can't be refunded! Breaks the contract silently or loudly.
        raise NotImplementedError("Gift cards cannot be refunded")


def process_refund(payment_method: PaymentMethod, amount):
    payment_method.refund(amount)   # crashes unexpectedly for GiftCardPayment!

process_refund(CreditCardPayment(), 50)   # Works
process_refund(GiftCardPayment(), 50)     # 💥 Crashes — violates LSP
```

**Problem:** Code written against the `PaymentMethod` abstraction assumes **every** subclass can `refund()`. `GiftCardPayment` silently breaks that assumption — any code that substitutes it in place of `PaymentMethod` can crash unexpectedly. This is a classic LSP violation.

### Fix: Redesign the hierarchy so the contract is honest

```python
class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount):
        ...

class RefundablePaymentMethod(PaymentMethod):
    @abstractmethod
    def refund(self, amount):
        ...

class CreditCardPayment(RefundablePaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via Credit Card")
    def refund(self, amount):
        print(f"Refunding ${amount} to Credit Card")

class GiftCardPayment(PaymentMethod):     # NOT refundable — doesn't claim to be
    def pay(self, amount):
        print(f"Charging ${amount} via Gift Card")


def process_payment(method: PaymentMethod, amount):
    method.pay(amount)                     # safe for ALL payment methods

def process_refund(method: RefundablePaymentMethod, amount):
    method.refund(amount)                  # only called on types that support it

process_payment(GiftCardPayment(), 50)          # Works fine
process_refund(CreditCardPayment(), 50)         # Works fine
# process_refund(GiftCardPayment(), 50)         # Type checker/reviewer catches this — GiftCardPayment isn't a RefundablePaymentMethod
```

**Why better:** The type hierarchy now **accurately reflects capability**. Any function that accepts `RefundablePaymentMethod` is guaranteed a working `refund()` — no subclass secretly breaks that promise. Substitutability is restored.


# I — Interface Segregation Principle (ISP)

**Definition:** Clients should not be forced to depend on methods they don't use. Prefer several small, specific interfaces over one large, general-purpose one.

### Violation: One fat interface forces unused methods on every implementer

```python
from abc import ABC, abstractmethod

class PaymentMethod(ABC):
    @abstractmethod
    def pay(self, amount): ...
    @abstractmethod
    def refund(self, amount): ...
    @abstractmethod
    def get_installment_plan(self, amount): ...   # only credit cards support this
    @abstractmethod
    def generate_qr_code(self): ...                # only UPI supports this


class UPIPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via UPI")
    def refund(self, amount):
        print(f"Refunding ${amount} via UPI")
    def get_installment_plan(self, amount):
        raise NotImplementedError("UPI doesn't support installments")  # forced, useless method
    def generate_qr_code(self):
        return "upi://pay?amount=..."


class CreditCardPayment(PaymentMethod):
    def pay(self, amount):
        print(f"Charging ${amount} via Credit Card")
    def refund(self, amount):
        print(f"Refunding ${amount} to Credit Card")
    def get_installment_plan(self, amount):
        return f"3 installments of ${amount/3:.2f}"
    def generate_qr_code(self):
        raise NotImplementedError("Credit cards don't use QR codes")   # forced, useless method
```

**Problem:** Every class is forced to implement methods that are irrelevant to it, resulting in ugly `NotImplementedError` stubs. This "fat interface" couples unrelated capabilities together.

### Fix: Split into small, role-specific interfaces

```python
class Payable(ABC):
    @abstractmethod
    def pay(self, amount): ...

class Refundable(ABC):
    @abstractmethod
    def refund(self, amount): ...

class InstallmentSupported(ABC):
    @abstractmethod
    def get_installment_plan(self, amount): ...

class QRCodeSupported(ABC):
    @abstractmethod
    def generate_qr_code(self): ...


# Each class implements ONLY what's relevant to it
class UPIPayment(Payable, Refundable, QRCodeSupported):
    def pay(self, amount):
        print(f"Charging ${amount} via UPI")
    def refund(self, amount):
        print(f"Refunding ${amount} via UPI")
    def generate_qr_code(self):
        return "upi://pay?amount=..."

class CreditCardPayment(Payable, Refundable, InstallmentSupported):
    def pay(self, amount):
        print(f"Charging ${amount} via Credit Card")
    def refund(self, amount):
        print(f"Refunding ${amount} to Credit Card")
    def get_installment_plan(self, amount):
        return f"3 installments of ${amount/3:.2f}"

class GiftCardPayment(Payable):     # only implements what it actually supports
    def pay(self, amount):
        print(f"Charging ${amount} via Gift Card")


# Usage: functions depend only on the capability they need
def checkout(payment: Payable, amount):
    payment.pay(amount)

def show_qr(payment: QRCodeSupported):
    print(payment.generate_qr_code())

checkout(GiftCardPayment(), 20)     # fine — GiftCard is Payable
show_qr(UPIPayment())                # fine — UPI is QRCodeSupported
# show_qr(CreditCardPayment())       # type checker flags this — Credit Card isn't QRCodeSupported
```

**Why better:** No class is forced to implement irrelevant methods or throw `NotImplementedError`. Code that only needs `pay()` depends only on `Payable` — not on refund, installment, or QR logic it doesn't care about.


# D — Dependency Inversion Principle (DIP)

**Definition:** High-level modules should not depend on low-level modules — **both should depend on abstractions**. Abstractions should not depend on details; details should depend on abstractions.

### Violation: High-level `PaymentService` tightly coupled to a concrete class

```python
class StripeGateway:
    def charge(self, amount):
        print(f"Charging ${amount} via Stripe API")


class PaymentService:
    """High-level business logic — but directly depends on a LOW-level, concrete class."""
    def __init__(self):
        self.gateway = StripeGateway()     # hard-coded dependency!

    def checkout(self, amount):
        self.gateway.charge(amount)


service = PaymentService()
service.checkout(100)
# To switch to Razorpay or PayPal, you must edit PaymentService itself — tight coupling.
```

**Problem:** `PaymentService` (high-level policy/business logic) directly instantiates `StripeGateway` (a low-level implementation detail). Swapping providers, mocking for tests, or supporting multiple gateways all require modifying `PaymentService`.

### Fix: Both depend on an abstraction, dependency is injected

```python
from abc import ABC, abstractmethod

class PaymentGateway(ABC):        # the abstraction both sides depend on
    @abstractmethod
    def charge(self, amount): ...


class StripeGateway(PaymentGateway):     # low-level detail
    def charge(self, amount):
        print(f"Charging ${amount} via Stripe API")

class RazorpayGateway(PaymentGateway):   # another low-level detail
    def charge(self, amount):
        print(f"Charging ${amount} via Razorpay API")

class FakeGateway(PaymentGateway):       # test double — trivial because of DIP
    def charge(self, amount):
        print(f"[TEST] Pretending to charge ${amount}")


class PaymentService:
    """High-level module depends only on the PaymentGateway abstraction."""
    def __init__(self, gateway: PaymentGateway):
        self.gateway = gateway            # injected, not hard-coded

    def checkout(self, amount):
        self.gateway.charge(amount)


# Usage — swap implementations freely, no PaymentService changes needed
service = PaymentService(StripeGateway())
service.checkout(100)

service_rzp = PaymentService(RazorpayGateway())
service_rzp.checkout(200)

# Trivial to test in isolation:
test_service = PaymentService(FakeGateway())
test_service.checkout(50)
```

**Why better:** `PaymentService` never changes regardless of which gateway is used. New gateways plug in without touching business logic. Unit testing is trivial — inject a `FakeGateway` instead of hitting a real payment API.




