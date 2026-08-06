
### Q1: What is the difference between service and application?


**Service** : A service is a program that runs in the background and provides functionality to the operating system. Services usually start automatically when the system boots when requested.



**Application** : An application is software that users run to perform specific tasks. It typically provides a graphical or command-line interface and starts only when the user launches it.

| Feature              | Service                                                                                     | Application                                                           |
| -------------------- | ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------- |
| **Definition**       | A background program that provides functionality to other programs or the operating system. | A program designed for direct interaction with the user.              |
| **User Interaction** | No direct user interface; runs in the background.                                           | Has a graphical user interface (GUI) or command-line interface (CLI). |
| **Execution**        | Starts automatically during system boot or when requested.                                  | Started manually by the user.                                         |
| **Purpose**          | Performs continuous tasks or provides services to other software.                           | Performs specific tasks for the user.                                 |
| **Dependency**       | Can run independently without user login.                                                   | Usually requires a user to launch and interact with it.               |
| **Lifetime**         | Runs continuously until stopped.                                                            | Runs until the user closes it.                                        |
| **Examples**         | Web server, database server, SSH server.                                                    | Web browser, text editor, media player, calculator.                   |


<br>
<br>

### Q2: What are these wildcards ~, ., .., * and ? ?

**WildCard** : A wildcard is a special character used in the shell to match one or more filenames or directory names based on a pattern, instead of specifying the exact name.


**'~'(Tilde)** : This '~' symbol represents the home directory of the current user.

**example:**
input : echo ~ 
output : /home/xull 

input : ~/Downloads
output : /home/xull/Downloads


**'.' (Current Directory)**: This '.' symbol represents the current working directory.


**example** input: ls .
  output : Desktop  Documents  Downloads  Music  Pictures  Public  PyCharmMiscProject  Templates  Videos  idea  snap  webstorm

  **'..' (Parent Directory):** This '..' symbol represents the parent directory of current working directory (one level above the current directory).

**example** input pwd  
output: /home/aniket/Documents/Projects
 input: cd..

 input: pwd 
 output: /home/aniket/Documents

 <br>
 <br>

 **'*'(Asterisk Wildcard)**: This '*' (Asterisk Wildcard) wildcard matches zero or more characters.

 **examples**


input: ls *.txt

output:
notes.txt  
report.txt  
hello.txt  

**'?' (Question Mark Wildcard):** This '?'  wildcard matches only one characters.
**example**  
suppose the directory contains:  

a.txt  
b.txt  
ab.txt  
abc.txt  
1.txt  

Ccommand:  

ls ?.txt  

matches:  

a.txt  
b.txt  
1.txt  

does not match:  

ab.txt  
abc.txt  
  

### What are the different flags for kill? Why do we use kill -9 in general?

The kill command in Linux is used to terminate processes—it can also pause, continue, reload, or otherwise control them by sending different signals.
-9 is a flag that is used to terminate processes forcefully.

**example**  
Gracefully terminate a process (default)
kill 1234 
 or 
 kill -15 1234  

 Forcefully terminate a process
kill -9 1234    


### Q4. Are you clear about file permissions? Explain them? chmod and chown commands?

File permissions are one of the most fundamental security features in Linux. They determine who can read, write, or execute a file or directory.


# Types of Permissions

Linux defines three basic permissions.  
| Permission | Symbol | Octal_Value |
|------------|:------:|:-----:|
| Read       | r      | 4     |
| Write      | w      | 2     |
| Execute    | x      | 1     |


# Permission Categories

Permissions are assigned to three classes of users.

| Category | Symbol | Description |
|----------|:------:|-------------|
| User (Owner) | `u` | The owner of the file |
| Group | `g` | Members of the file's group |
| Others | `o` | Everyone else |
| All | `a` | User, Group, and Others together |


**chmod:** The chmod (change mode) command changes the permissions of files and directories.  
**Numeric Mode Examples**  
chmod 600 file.txt  
**Symbolic Mode Examples**  
chmod o+rw file.txt  
chmod u=rw file.txt

**chown:** The chown (change owner) command changes the owner and/or group of a file or directory.  
Only the root user or a user with appropriate privileges can change file ownership.

**example**  

Change the owner:  

sudo chown alice report.txt  

Change the owner and group:  

sudo chown alice:developers report.txt  

### Q5. Usage of Ctrl+R to search previously run commands, arrow keys, tab autocompletion.

**Ctrl + R (Reverse Search Command History):**  

Ctrl + R performs a reverse incremental search through your shell command history. It searches previously executed commands as you type, allowing you to quickly find and reuse old commands.

Instead of scrolling through hundreds of commands, you can search by entering part of a command.
How to Use
Press Ctrl + R.
Type part of a previous command.
The shell displays the most recent matching command.
Press Enter to execute it or use the arrow keys to edit it before execution.


**Arrow Keys**

The Up and Down arrow keys allow you to navigate through your command history.  

**Tab Autocompletion**

The Tab key automatically completes file names, directory names, and commands.

It helps avoid typing mistakes and speeds up command entry.



