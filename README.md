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

- At the very top of the file system is the `root directory`, which holds everything else.
- It is referred to using the `/` character.
- It would be the leading slash in `/Users/joon.k` on my computer.
- Only the leading slash indicates the root directory. If it appears inside a path, it is a separator.

- Typically, when a new command prompt is opened, it will open the home directory to begin with.
- You could use the `ls` command to get the list of all the contents stored in the home directory.

### Getting Help

- `ls` has many options, such as `ls -F`, which will list each content with a marker to indicate the type of each content.
  - a trailing `/` indicates a directory (folder)
  - `@` indicates a link
  - `*` indicates an executable

- In order to find out more options, use `man ls`, which is 'manual listing' (for macOS)
  - to search for a character or word in this page, use `/` followed by the character or word you are searching for.
  - If there are multiple hits, use `N` to move forward, and `Shift + N` to move backward.
  - Hit `Q` to exit.

- Some other options for `ls` are:
  - `-l`: long list format. Includes file size, time of last mod, etc.
  - `-h`: makes information more 'human-readable'
  - `-t`: `ls` lists items alphabetically by default. `-t` will list the items by time of last mod.
  - `-r`: lists items in reverse order
- NOTE: options may be combined to view lists in desired format/order (ex. `ls -rtl`)

### Exploring Other Directories

- `ls` can be used to list the contents of a different directory.
- `ls -F Desktop` will list the items on the `Desktop`, where `Desktop` is the argument.
- NOTE: Using this command will not change the `current working directory`. It only lists the contents of the 'argument' folder specified.

- Currently, `ls -F Desktop` will list `shell-lesson-data/` which has a trailing slash indicating it is a folder.

- In order to look at what is inside `shell-lesson-data/`, there are two methods.
  - `ls -F Desktop/shell-lesson-data` will simply list the contents of `shell-lesson-data` without changing the current working directory
  - `cd` (change directory) following by the target directory name will change the current working directory. (Like double-clicking a folder icon to open it)
  - `cd shell-lesson-data` will change the CWD to 'shell-lesson-data'. Here we can use `ls` command to list the contents of the CWD 
  - `exercise-data/  north-pacific-gyre/`
  - Note that you cannot jump directly into the `exercise-data/` from the `Desktop`.
    - `cd Desktop`
    - `cd shell-lesson-data`
    - `cd exercise-data`
  - `pwd` command will print `/Users/joon.k/Desktop/shell-lesson-data/exercise-data`

- Entering `cd shell-lesson-data` from the previous CWD in an attempt to move up in the directory tree will throw an error message.
- This is because `cd` can only see into sub-directories.
- Use `cd ..` to move up one directory.
- Entering `cd` command any time in the shell will return to the home directory, which is useful when you get lost in the file system.