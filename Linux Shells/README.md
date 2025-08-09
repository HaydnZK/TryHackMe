# Linux Shells
## Overview
This room covers how to interact with a shell, the common Linux shells you’ll encounter, and basic shell scripting components and examples.

## Interacting with a shell
- By default your shell starts in your home directory.

- Check the current directory with pwd

- Change directories with cd <directory>

- List directory contents with ls

- Read file contents with cat <filename>

- Search inside files with grep <pattern> <file>

Example: grep THM dictionary.txt searches for the string THM inside dictionary.txt

Note: when you run commands you are operating in the current working directory. Make sure you are in the folder you expect before creating, editing, or executing files.

## Types of Linux shells
- See which shell you are using with echo $SHELL

- List installed shells with cat /etc/shells

- Switch shells by typing the shell name, for example zsh

- Change your default shell permanently with chsh -s /usr/bin/zsh

### Common shells covered:

- Bourne Again Shell (bash)

Default on most distributions

Strong scripting capabilities

Tab completion for commands and filenames

Command history (use arrow keys or history)

- Friendly Interactive Shell (fish)

Focused on usability and readable default syntax

Autocorrect for commands

Prompt themes and syntax highlighting

Provides tab completion and command history

- Z Shell (zsh)

Modern shell with advanced tab completion and scripting support

Autocorrection and extensive customization options

Offers tab completion and history like other shells (custom themes/plugins available)

## Shell scripting and components
- Create a script file with an editor, for example nano first_script.sh

- Every script should start with a shebang to define the interpreter, for example #!/bin/bash

Example: simple interactive script
#!/bin/bash
echo "Hey, what's your name?"
read name
echo "Welcome, $name"

Save the file (in nano: Ctrl+X, Y, Enter), then make it executable:
chmod +x first_script.sh

Execute the script from the current directory:
./first_script.sh

Notes on execution: using ./ tells the shell to run the script in the current directory. If you omit ./, the shell searches the directories in your PATH and may not find the script.

### Loops
Example script to print numbers 1 to 10
#!/bin/bash
for i in {1..10}; do
echo $i
done

Run with:
./loop_script.sh

### Conditionals
Example script using an if statement
#!/bin/bash
echo "Please enter your name first:"
read name
if [ "$name" = "Stewart" ]; then
echo "Welcome, Stewart! Here is the secret: THM_Script"
else
echo "Sorry! You are not authorized to access the secret."
fi

Example outputs:

- If input is Stewart: Welcome, Stewart! Here is the secret: THM_Script

- If input is Alex: Sorry! You are not authorized to access the secret.

### Comments
- Use # at the start of a line to add comments and document intent inside scripts

## The locker script (practical example)
This example combines loops and conditionals to collect username, company name, and PIN, then checks them.

Script outline:
#!/bin/bash

Define variables:
username=""
companyname=""
pin=""

Prompt loop:
for i in {1..3}; do
if [ "$i" -eq 1 ]; then
echo "Enter your Username:"
read username
elif [ "$i" -eq 2 ]; then
echo "Enter your Company name:"
read companyname
else
echo "Enter your PIN:"
read pin
fi
done

Final check:
if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
echo "Authentication Successful. You can now access your locker, John."
else
echo "Authentication Denied!!"
fi

Sample run when PIN is wrong:
Enter your Username:
John
Enter your Company name:
Tryhackme
Enter your PIN:
1349
Authentication Denied!!
