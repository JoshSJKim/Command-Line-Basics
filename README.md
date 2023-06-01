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

## Create a Text File

- Open up a new file `draft.txt` with the `nano` text-editor in the desired directory by entering `$ nano draft.txt`
- Enter some text in the opened text editor. When done, press `control + O (letter 'O')` to save.
- You could choose the name of the file and press `return` or `enter` to save.
- Press `control + X` to close the editor and return to the shell.
- `nano` doesn't leave any output on the shell display screen after it exits. But `ls` command will show that `draft.txt` has been created in the `thesis` folder.

- NOTE: `control` + `[key]` can be described as `control+x`, `control-x`, `Ctrl+X`, `Ctrl-X`, `^X`, or `C-x`

- Another way to create a new file is `touch` command
  - `$ touch my_file.txt` will create a new blank `my_file.txt` file, which has a file size of 0 bytes.
  - In order to remove a file (not a directory), use the `rm` command
    - `$ rm my_file.txt` will remove the `my_file.txt` file from the `thesis` folder

## Moving Files and Directories

- The `mv` command can either `rename` or `move` a file or directory

### Rename a File

- `$ mv thesis/draft.txt thesis/quotes.txt` will change the name of `draft.txt` to `quotes.txt`.
  - This command has the same effect as `renaming` a file or directory on a GUI environment.
  - Note that `mv` will silently overwrite any existing file with the same name by default, which could lead to data loss. Use caution.
  - However, `mv -i` ('i' for 'interactive') will trigger `mv` to request a confirmation.

### Moving Folders

- `$ mv thesis/quote.txt .` will move the renamed `quotes.txt` from the `thesis` directory to the current working directory (specified by `'.'`), which is the `writing` directory.
- If you try to access `quotes.txt` in `thesis`, --> `$ ls thesis/quote.txt`, it would return `No such file or directory`.

- Note: `ls` with a filename or a directory as an argument only lists the requested file or directory.
  - This can be useful to confirm that the specified file or directory is present in the current working directory.

```CLI
$ ls -F
  analyzed/ raw/                                    --> current working folder has two directories 'analyzed' and 'raw'
$ ls -F analyzed                                    --> 'analyzed' directory contains the following files.
fructose.dat glucose.dat maltose.dat sucrose.dat 
$ cd analyzed                                       --> change directory to 'analyzed'.
```

In order to move the 'maltose.dat' and 'sucrose.dat' files to the 'raw' directory, use the following command

`$ mv sucrose.dat maltose.dat ../raw` --> `..` will move the working directory up by one (the parent folder), and the second argument specifies which directory to put the specified files.

## Copying Files and Directories

### Copy a File and Save in another folder

- `cp` command works similar to `mv`, except it copies a file instead of moving it.

- `$ cp quotes.txt thesis/quotations.txt` will copy `quotes.txt` and save the copied file `quotations.txt` in the `thesis` directory.
- `$ ls quotes.txt thesis/quotations.txt` will confirm that both files are present in the file system.

### Copy a Directory and all its contents

- Copy a directory and all its contents by using the `recursive` option `-r`, which is useful for backing up a folder.
- `$ cp -r thesis thesis_backup` will create a copy of the `thesis` directory under the name `thesis_backup` and save it in the current working directory.
- `$ ls thesis thesis_backup` will confirm that it is indeed a duplicate.

## Removing Files and Directories

- Remove files by using the `rm` command
- `$ rm quotes.txt` will remove the `quotes.txt` file from the file system, permanently.

- Note that the shell environment does not have a trash bin. The removed files cannot be recovered.
  - In order to ensure that only unwanted files are removed (not others by mistake), use the `-i` option to bring up a prompt to confirm removal.
  - `$ rm -i thesis_backup/quotations.txt` will bring up the following prompt
    - `rm: remove regular file 'thesis_backup/quotation.txt'? y` --> press `Y` to confirm removal or `N` to cancel removal.

- `rm` command on its own, by default, only removes 'files', not 'directories'.
- `rm` can remove a directory and all of its contents with the use of the recursive option `-r`.
  - This also removes the directory without confirmation prompts.

- Whenever removing a file or a directory, make it a habit to include the `-i` option to confirm removal.

## Operations with Multiple Files and Directories

- Copying or moving multiple files at once can be done by providing a list of individual file names, OR specifying a naming pattern using `wildcards`.
- `Wildcards` are special characters that can be used to represent unknown characters or sets of characters when navigating the file system.

### Copy with multiple file names

- You can copy multiple files and save it in a different directory by using `$ cp someDir/[filename.ext] ... someOtherDir/`
- It doesn't matter how many files you copy, as long as the last argument is a directory that the copied files will be saved in.

### Using Wildcards for Accessing Multiple Files at Once

- `*` represents zero or more other characters.
  - For example, `*.pdf` represents all files in a directory that has the `.pdf` extension.
  - `p*.pdb` represents all files with a `.pdb` extension that begins with the letter `p`.
- `?` represents exactly one character
  - For example, `?ethane.pdb` represents all files with a `.pdb` extension with a file name that ends in `ethane` and begins with any letter.

- Wildcards can be used in combination.
  - `???ane.pdb` represents all files with a `.pdb` extension that begin with three characters and ends in `ane`

- Note: When the shell sees a wildcard, it expands the wildcard to create a list of matching filenames PRIOR TO running the preceding command.
- If a wildcard does not find a match, it will pass the expression as an argument to the command as is.

## KeyPoints

- `cp [oldName] [newName]` copies a file.
- `mk [path]` creates a new directory
- `mv [oldName] [newName]` renames (or moves) a file or directory
- `rm [path]` deletes a file (remember `-r` option to delete a directory and `-i` option to provide a prompt for deletion)
- `*` matches ZERO or more characters in a filename
- `?` matches any single character in a filename
- Remember there are various ways of describing the `control` key (`Control`, `Ctrl`, `^`)
- The shell does not have a trash bin (remember the `-i` option)
- Most file names include an extension, but it is not necessary.
- 