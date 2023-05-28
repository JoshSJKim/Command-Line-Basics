# Command-Line-Basics

## What is a command shell (or Command Line Interface - CLI)

- CLI is a text-based interface that allows you to interact with a computer's OS by entering commands.
- A direct line of communication with the computer: give it instructions and get responses.
- It's like a virtual assistant that carries out tasks such as creating folders, copying files, launching programs, or configuring system settings.
- It is more efficient and manageable compared to the GUI approach because it performs tasks quickly and redundant actions can be automated.

- When the shell is first opened, it presents a `prompt`, which indicates that the shell is waiting for an input, or command.
- The shell typically uses `$`as the prompt, but may use a different symbol depending on the shell (most popular is BASH. I have `zsh` installed)
- DO NOT TYPE THE PROMPT when entering commands.

### ls (listing)

- `ls` command will list the contents of the current working directory (CWD)

- Using the command shell, it is possible to:
  - navigate to a file/directory
  - create a file/directory
  - check the length of a file
  - chain commands together
  - retrieve a set of files
  - iterate over files
  - run a shell script containing her pipeline

## NOTE

- A shell is a program whose primary purpose is to read commands and run other programs
- The shell's main advantages are its high action-to-keystroke ratio, its support for automating repetitive tasks, and its capacity to access networked machines.
- Main disadvantages are its primarily textual nature and non-intuitive appearance.

## Navigating Files and Directories (folders)

- The part of the OS responsible for managing files and folders is called the `file system`.
- It organizes data into files that hold information, and directories (folders) that hold files and/or other directories.

- Use the command `pwd (print working directory)` to find out the current working directory.
- Directories are like 'places'. Within a shell, we are in exactly one place at any given time.
- Commands mostly write and read files in the CWD.
- It is important to know 'where I am' before running a command.

