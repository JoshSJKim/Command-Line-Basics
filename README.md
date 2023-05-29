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

- Note that directories could be strung together to reach the desired directory in one command.
- `cd Desktop/shell-lesson-data/exercise-data` will directly change the directory to `exercise-data`.
  - Here we can use `ls -F` to list the contents of `exercise-data` with the indication of the type of each content.

- To move up a directory, as mentioned earlier, we could use `cd ..` to achieve this.
- This is because we have been using `relative paths` until now.
- It is possible to specify an `absolute path` to move to any directory in the file system by entering the exact location of the desired directory starting from the `root directory`, which can be done by entering the directory path starting with a `/`.
- Use `pwd` to find out exactly where I am in the file system, and then enter the desired directory starting with the root directory.

`cd /users/joon.k/Desktop/shell-directory`

### Two More Shortcuts

- tilde (`~`): means 'the current user's home directory' only if used at the beginning of the path
  - if home directory is `/Users/joon.k`, `~/Desktop` is equivalent to `/Users/joon.k/Desktop`
- dash(`-`): `cd -` will translate in to 'the previous directory'.
  - Useful when moving back and forth from two directories.
- Summary: `~` means home directory, `..` moves `up` the directory tree, `-` moves `back` to the previous directory.

## General Syntax of a Shell Command

Example

`$ ls -F /`

- `$` is the prompt (Not all shell have this syntax. The prompt should not be typed in)
- `ls` is the command.
- `-F` is the option
- `/` is the argument

- options and arguments are sometimes referred to as `parameters`.
- A command can be called with more than one option and more than one argument
- A command doesn't always require an argument or an option.
- `options` are sometimes referred to as `switches` or `flags`.
- Each component of a command must be separated with a space.
- letter casing is also important
  - `-s` will display size of files
  - `-S` will sort the files and directories by size.

## Tab Completion

- In my file system, I am currently in `/Users/joon.k/Desktop/shell-lesson-data`.
- There are two more folders inside this directory `exercise-data` and `north-pacific-gyre`.
- In order to list the contents of the `north-pacific-gyre` folder, we use the `ls` command.
- But it is tiresome to always have to type out `north-pacific-gyre`.
- Simply enter `ls nor` and hit the `tab` button, and the shell automatically completes the directory name.
- This is called tab completion.
- `ls north-pacific-gyre/` will be completed.
- If `tab` is pressed again, it will display the files within that folder.
- If `G` is pressed --> `ls north-pacific-gyre/g` and then `tab` is pressed, it will automatically append --> `ls north-pacific-gyre/goo` since all of the files that start with `g` in this folder share the first three characters 'goo'.
- If `tab` is pressed once more, it will print all the files that begin with 'goo'.


### Summary

- The file system is responsible for managing information on the disk.
- Information is stored in files, which are stored in directories (folders).
- Directories can also store other directories to form a directory tree.
- `pwd` prints the user's current working directory.
- `ls` prints the contents of the current working directory.
- `ls [path]` prints the contents of the specified path (without changing the current working directory).
- `cd [path]` changes the current working directory.
- Most commands take options that begin with a single `-`.
- Directory names in a path are separated with `/`.
- `/` on its own is the root directory of the entire file system. `/` in `/Users` refers to the `root directory`.
- A relative path specifies a location starting from the current working location.
- `.` on its own means 'the current directory'. `..` means 'the directory above the current directory'.

## Working with Files and Directories

### Creating Directories

- use `mkdir [newDirectoryName]` to create a new directory.
- It will create a new directory in the current working directory.

- We are currently in `/Users/joon.k/Desktop/shell-lesson-data`
- `cd exercise-data/writing` will change directory to the `writing` folder in `exercise-data`
- in `writing`, create a new directory called `thesis` by entering `mkdir thesis`.
- `ls -F` command will list `LittleWomen.txt  haiku.txt  thesis/`, where `thesis` is an empty directory that's just been created.

- It is possible to create a new directory with nested sub-directories using a single command with `-p`.
  - `$ mkdir -p ../project/data ../project/results` will create a new directory called `project` in the previous (`..`) working directory, which also has two nested sub-directories named `data` and `results`.
- `ls -FR ../project` will list the contents of the newly created `project` directory.

### Naming Files and Directories

- It is important to create file and directory names that are easy to work with.

- Do not use spaces
  - spaces are used to separate arguments on the command line. It is better to avoid them in names of files and folders.
  - Use `_` or `-`, or even camelCasing.
- Do not begin with `-`
  - Commands treat names beginning with `-` as options.
- Stick with numbers, letters, period or 'full stop' (`.`), dash (`-`), and underscore (`_`).
  - Many characters have special meaning in the command line and could cause unexpected results if used in a file or directory name.

- If it is necessary to refer to names or folders that use spaces or special characters, surround the names in quotes (`""`)