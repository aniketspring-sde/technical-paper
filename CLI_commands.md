
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


**'~'(Home Directory)** : This '~' symbol represents the home directory of the current user.

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
 







References :
Q1 : https://simplicable.com/IT/application-vs-service, https://superuser.com/questions/1064402/what-is-the-difference-between-a-service-and-an-application
