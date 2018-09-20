#!/usr/bin/env python3

import os
import sys


def execute_process(command):
    paths = os.environ['PATH'].split(':')
    args = command.split(' ')

    # Try command as is
    try:
        os.execve(args[0], args, os.environ)
    #Try catch for error handling if command is not valid
    except FileNotFoundError:
        for path in paths:
            try:
                os.execve(path + "/" + args[0], args, os.environ)
            except FileNotFoundError:
                pass

        print("Command not found")

#main method
def main():
    print()
    print("JC_Shell Started")

    while True:
        command = input("$ ").rstrip().lstrip()
        pipeCommand = command.split("|")

        if command.startswith("cd"):
            chdir_command = command.split(" ")
            os.chdir(chdir_command[1])

        # to run in the background
        elif command.endswith("&"):
            command = command[:-1].rstrip()
            execute_command_background(command)

        # to pipe command
        elif len(pipeCommand) > 1:
            output_command = pipeCommand[0].rstrip().lstrip()
            input_command = pipeCommand[1].rstrip().lstrip()

            pipe_command(output_command, input_command)
        elif command == 'exit':
            print("Exiting shell")
            break
        elif not command:
            continue
        else:
            execute_command(command)


def execute_command(command):
    newpid = os.fork()
    if newpid == 0:
        execute_process(command)
    else:
        pids = (os.getpid(), newpid)
        os.waitpid(pids[1], 0)


def execute_command_background(command):
    newpid = os.fork()
    if newpid == 0:
        execute_process(command)


def pipe_command(output_command, input_command):

    # Work in progress as pipe wasnt fully fiunctional, half way as in
    # i was able to implement the process where it is writing the output
    # to a file of the first command and named it output and being
    # unsuccessfull to pipe that command

    pid = os.getpid()  # get and remember pid

    r, w = os.pipe()
    for f in (r, w):
        os.set_inheritable(f, True)

    import fileinput

    new_pid = os.fork()

    if new_pid == 0:  # Child Process
        os.close(1)  # redirect child's stdout
        os.dup(w)
        for fd in (r, w):
            os.close(fd)
        print("k")
        #os.execve("/bin/ls", ["/bin/ls"], os.environ)
    else:
        os.close(0)
        os.dup(r)
        for fd in (w, r):
            os.close(fd)
        for line in fileinput.input():
            print("From child: <%s>" % line)


if __name__ == '__main__':
    main()
