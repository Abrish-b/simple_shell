# Welcome to Ethio - Simple Shell!

A simple UNIX command interpreter written as part of the low-level programming and algorithm track at Holberton School.


#  Description

**Ethio** is a simple UNIX command language interpreter that reads commands from either a file or standard input and executes them.

## Invocation

Usage:  **Ethio**  [filename]

To invoke  **Ethio**, compile all  `.c`  files in the repository and run the resulting executable:

**Ethio** can be invoked both interactively and non-interactively. If **Ethio** is invoked with standard input not connected to a terminal, it reads and executes received commands in order.

If **Ethio** is invoked with standard input connected to a terminal (determined by [isatty](https://linux.die.net/man/3/isatty)(3)), an _interactive_ shell is opened. When executing interactively, **Ethio** displays the prompt `$` when it is ready to read a command.

### Environment

Upon invocation,  **Ethio**  receives and copies the environment of the parent process in which it was executed. This environment is an array of  _name-value_  strings describing variables in the format  _NAME=VALUE_. A few key environmental variables are:

#### [](https://github.com/Abrish-b/simple_shell/README.md#home)HOME
The home directory of the current user and the default directory argument for the  **cd**  builtin command.
#### PWD
The current working directory as set by the  **cd**  command.
#### PATH
A colon-separated list of directories in which the shell looks for commands. A null directory name in the path (represented by any of two adjacent colons, an initial colon, or a trailing colon) indicates the current directory.

### Command Execution
After receiving a command,  **Ethio**  tokenizes it into words using  `" "`  as a delimiter. The first word is considered the command and all remaining words are considered arguments to that command.  **Ethio**  then proceeds with the following actions:

1.  If the first character of the command is neither a slash (`\`) nor dot (`.`), the shell searches for it in the list of shell builtins. If there exists a builtin by that name, the builtin is invoked.
2.  If the first character of the command is none of a slash (`\`), dot (`.`), nor builtin,  **Ethio**  searches each element of the  **PATH**  environmental variable for a directory containing an executable file by that name.
3.  If the first character of the command is a slash (`\`) or dot (`.`) or either of the above searches was successful, the shell executes the named program with any remaining given arguments in a separate execution environment.

### Exit Status
**Ethio**  returns the exit status of the last command executed, with zero indicating success and non-zero indicating failure.

If a command is not found, the return status is  `127`; if a command is found but is not executable, the return status is 126.

All builtins return zero on success and one or two on incorrect usage (indicated by a corresponding error message).
### Signals
While running in interactive mode,  **Ethio**  ignores the keyboard input  `Ctrl+c`. Alternatively, an input of end-of-file (`Ctrl+d`) will exit the program.

User hits  `Ctrl+d`  in the third line.
### Variable Replacement
**Ethio** interprets the `$` character for variable replacement.
#### $ENV_VARIABLE

`ENV_VARIABLE`  is substituted with its value.
#### $?
`?` is substitued with the return value of the last program executed.
#### $$

The second  `$`  is substitued with the current process ID.
### Comments
**Ethio** ignores all words and characters preceeded by a `#` character on a line.
### Operators
**Ethio**  specially interprets the following operator characters:

#### [](https://github.com/Abrish-b/simple_shell/README.md#---command-separator); - Command separator
Commands separated by a  `;`  are executed sequentially.
#### && - AND logical operator
`command1 && command2`:  `command2`  is executed if, and only if,  `command1`  returns an exit status of zero.
#### || - OR logical operator
`command1 || command2`:  `command2`  is executed if, and only if,  `command1`  returns a non-zero exit status.
The operators `&&` and `||` have equal precedence, followed by `;`.
### Ethio Builtin Commands
#### cd
-   Usage:  `cd [DIRECTORY]`
-   Changes the current directory of the process to  `DIRECTORY`.
-   If no argument is given, the command is interpreted as  `cd $HOME`.
-   If the argument  `-`  is given, the command is interpreted as  `cd $OLDPWD`  and the pathname of the new working directory is printed to standad output.
-   If the argument,  `--`  is given, the command is interpreted as  `cd $OLDPWD`  but the pathname of the new working directory is not printed.
-   The environment variables  `PWD`  and  `OLDPWD`  are updated after a change of directory.
#### alias
-   Usage:  `alias [NAME[='VALUE'] ...]`
-   Handles aliases.
-   `alias`: Prints a list of all aliases, one per line, in the form  `NAME='VALUE'`.
-   `alias NAME [NAME2 ...]`: Prints the aliases  `NAME`,  `NAME2`, etc. one per line, in the form  `NAME='VALUE'`.
-   `alias NAME='VALUE' [...]`: Defines an alias for each  `NAME`  whose  `VALUE`  is given. If  `name`  is already an alias, its value is replaced with  `VALUE`.
#### exit
-   Usage:  `exit [STATUS]`
-   Exits the shell.
-   The  `STATUS`  argument is the integer used to exit the shell.
-   If no argument is given, the command is interpreted as  `exit 0`.
#### env
-   Usage:  `env`
-   Prints the current environment.
#### setenv
-   Usage:  `setenv [VARIABLE] [VALUE]`
-   Initializes a new environment variable, or modifies an existing one.
-   Upon failure, prints a message to  `stderr`.
#### unsetenv
-   Usage:  `unsetenv [VARIABLE]`
-   Removes an environmental variable.
-   Upon failure, prints a message to  `stderr`.
## Authors
-   Abrham Bunaro <[Abrish-b](https://github.com/Abrish-b)>
-   Mentesinot Tegegn<[Mente-t](https://github.com/Mentesinot)>
## Acknowledgements
**Ethio** emulates basic functionality of the **sh** shell. This README borrows form the Linux man pages [sh(1)](https://linux.die.net/man/1/sh) and [dash(1)](https://linux.die.net/man/1/dash).
