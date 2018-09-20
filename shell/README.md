

# Lab#1 Shell

**Purpose:**

Mimic a shell and its basic commands such as reading commands from the command line and being

able to tell the user if the command/path is either valid or invalid.

Demonstrate the ability to be able to apply Fork(), be able to expand children from parent processes.

Also be able to apply pipe(), wait() and both open() and close().



The user should be able to manipulate the shell in a way where the shell can understand the following:

- simple commands (e.g. $ /bin/ls or $ ls )
- simple pipes (e.g. $ /bin/ls | /bin/sort -r)
- background tasks (e.g. $ find /etc -print &amp; )
- &quot;cd&quot; ## for &quot;cd&quot; you will need to lookup the library routine &quot;chdir&quot; in the (online) unix manual

JCShell lab uses the following posix calls:

- pipe()
- fork()
- dup() or dup2()
- execve()
- wait()
- pen() and close()
- chdir()

# Using the program

Note: Its best to be ran through an IDE as the program was constructed using PyCharm.

Program was constructed using IDE PyCharm. Provided in the repo is the &quot;Shell.py&quot; which is the main program and could be loaded using PyCharm and be ran through its console. Also, as requested by the Dr. Freudenthal, it can also be ran standalone.

Once the shell has been run and is running, it will display &quot;JC\_Shell Started&quot; along with the &quot;$&quot;. This means shell is ready for input(commands).

Pipe(), Fork() and Dup() are used within the function called &quot;pipe\_command&quot;. This function was meant to pipe command and currently has flaws. I was able to implement the process where its writing the output to a file of the first command named output and being unsuccessful to pipe that command.

Execve() is within the function called &quot;execute\_process&quot;. I was able to make the shell recognize the command and if the command wasn&#39;t valid, the try/catch would catch the error and let the user know the command was invalid.

Wait() is located within the command function and is being utilized mostly for commands that are being made in the background.

Open() &amp; Close() like any other function will let you open/close .py files within the shell or the directory in where the shell is currently working on.

Chdir() is within the main function of the program and lets you change directories if so wished by concatenating &quot;cd&quot; to the front of any inputted command, that is if the command is valid.

Extras: shell provides the ability to the user to back track &quot;cd&quot; and &quot;cd ..&quot;

# Files in Directory

Shell.py – the program itself

Test.py – program code acquired from Dr. Freudenthals to demonstrate pipes and its functionalities.

BackgroundProcessTest.py – used for testing the shell and its capabilities to run commands in the back ground. This was proposed.

testShell.sh - provided by Dr. Freudenthal to test the shell

testFolder(Folder) -  Folder for testing purposes to verify shell did access directory as well access the directory inside testFolder directory.