# WeirdShell
An operating systems class assignment to create a basic Unix-shell with a few unique properties.

The unique properties:
- redirection and piping is implemented right-to-left, not left-to-right when typing a command
  Ex: instead of "cat file.txt | grep test > out.txt", use "out.txt < grep test | cat file.txt"
- if the characters 'c', 'm', 'p', or 't' appear in stdout, those characters should be duplicated
  Ex: "cats are cool" turns into "ccatts are ccool"

To run the shell, execute these commands in the WeirdShell dir:
    1. "make"
    2. "build/wrdsh"
You should now have entered the shell.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Outline of how we implemented the shell:

struct Single_Command:
- there is a command structure that keeps track of one simple command
(i.e. "ls -l") and holds the outfile if there is redirection

parse_input():
- once the shell has taken input from the user, we parse the input based
on whitespace

check_redirection():
- is called when we need to ensure that redirection is entered correctly
by the user

create_commands():
- next we split the command(s) based on any redirection symbols or pipes
found and put each simple command within its own struct
- each command struct is placed inside an array of command structs
- next we reverse the order of commands so that they will be executed
in proper order

set_up_execution():
- this is where we make the redirection changes if necessary based on 
the number of commands found in the array structure
- calls execute_command() once redirection for each pipe is set set_up

execute_command():
- executes one simple command and makes any necessary duplication of 
cmpt characters

All of these commands are called and set up within main().
main():
- keeps running the shell as long as "exit" hasn't been 
inputted
- frees memory when necessary

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Limitations/Notes:
- when allocating space for commands, we had a max size of the macro
BUFSIZ, so the user is limited with the amount of characters and commands
they can enter

- need to finish free-ing all of the memory

- the output redirection file will always be the first argument in 
the command line (if there is output redirection to a file)

- if the redirection symbol is found anywhere that isn't the second 
argument, will print an error message and the command will not be 
executed

- when the command "ls" is executed, it prints each file/dir on a newline
