# Commmand Line Exercise

Working in the command line can seem daunting at first, but this workshop is designed to get you comfortable with the environment. Work through these exercises in your own command line. If you want, you can make a separate file to note down things you learn or any questions you have.

-----

## Part 1: Commands and Arguments

### Exercise 1.1: Basic Command Execution and Whitespace

The shell separates commands and arguments based on whitespace.

First, open your terminal (or Git Bash terminal, or WSL terminal). Everything outlined here you will execute in your own terminal, so make sure you are in a directory where you are comfortable adding new files/directories!

1.  Create a directory named `bash_workshop` using the `mkdir` command and **navigate inside this new directory using the `cd` command**. (Make sure you understand where this directory is within your general directory structure!)
3.  Run the `ls` command to observe the initial directory state. What do you observe? 
4.  Use the `touch` command to create three files named `chipmunk1.txt`, `chipmunk2.txt`, and `chipmunk3.csv` in a single command, ensuring to separate each argument (file name) with a whitespace. Watch the file endings here! 
5.  Run `ls` again to confirm the files were created correctly.
6.  **Reflect:** Can you try to now make three different new files, this time separating them with varying numbers of white space? (e.g. `touch file1.txt             file2.txt`). Did the varying amount of whitespace between the filenames affect how `touch` interpreted the arguments? What does this mean for us when working with white spaces in the command line? 

### Exercise 1.2: Globbing and Flag Usage

A **glob** (like `*`) is a pattern that the shell expands into a list of filenames before the command executes.

Globbing is the process by which the shell expands these patterns into a list of matching file or directory names before the command is executed.

For example, you could list all the files of type `.csv` using the command `ls *.csv` (If you try this in your `bash_workshop` directory now, you should see only the `chipmunk3.csv` file we have created!). 

1.  Use a single `rm` command with a glob to delete all the files of type `.txt` in your current directory.
**Hint:** You can delete all files of type `.txt` with the command `rm *.txt`. 
2. List the contents of your directory to see what `rm` did. Did the glob work how you expected to? 


### Exercise 1.3: Quoting to Group Arguments

When arguments contain spaces, they must be quoted to be treated as a single unit.

1.  Execute the following command, noting the large number of whitespace. Observe the output:
    ```bash
    echo alvin        and          the chipmunks.
    ```
2.  Use the `echo` command again, but this time, wrap the entire sentence in **double quotes** (`"`).
3.  **Reflect:** In both cases, how many arguments did the `echo` command receive? What is the practical difference in the output? What is important to remember when working with strings that contain whitespaces?
 

### Exercise 1.4: Handling Filenames with Spaces

Working with files that contain spaces can be dangerous if quoting is omitted.

1.  Create a file named `Important File.txt` and a second file named `secret`.
**Tip:** It's always a good idea to double check where you are in your file system before altering files/directories. Double check that you are still in the `bash_workshop` directory we created earlier!
2.  **Dangerous Test:** Attempt to delete only `My Important File.txt` **without** surrounding the filename in quotes.
3.  Run `ls` to see which files remain.
4.  **Fix:** Now, delete the remaining file correctly by using **double quotes** around its filename.
5. **Reflect:** How should we deal with files containing whitespaces? Do you think naming files with whitespaces is a good idea when working in the command line? 

**Note:** What I want you to understand here is that the **number** of white spaces does not matter, the command line will always separate arguments by a singular white space. Why is this important? Often when working in graphical interfaces, we encounter file with a white space in their names, e.g. `CV Imperial 2025`. These types of file names containing white spaces are an absolute no-go when working in the command line, because if you forget to wrap them in `""` each time (which is frankly easy to do on accident), they will be interpreted as three separate files: `CV` and `Imperial` and `2025`. The best practice when naming files in the command line is to use underscores, capital letters, or dashes to miminic white spaces in file names, for example, you could name that file `CV_Imperial_2025` instead and save yourself a headache later on! 

-----

## Part 2: Moving Around Directories

### Exercise 2: Get Comfortable Moving Around in the Command Line

1.  Create a text file named `setlist.txt` using an editor with the following content (on separate lines):

    ```text
    You Spin Me Round
    Uptown Funk
    The Chipmunk Song
    ```

**Tip:** use nano, a simple editor built in to your command line, by using the command `nano setlist.txt`. Remember, to save and exit in nano, press Ctrl+O (Write Out) and then Ctrl+X (Exit).

**Challenge:** use Vim as your editor instead! 

2.  Run the command `ls` to check your work. You can further use `cat setlist.txt` to see the contents of the file to see that its contents were created properly. 

3. You now need to make an organized directory system for the upcoming tour. Make a new directory called `songs` and navigate inside it. 

4. Create the files `song1.mp3` `song2.mp3`. You can do this all in one line!

5. You want to send `song1.mp3` to a friend but forgot where the file is located! Use `pwd` to help see where you are in your file system. 

6. Use `cd ..` to navigate back to your parent directory. 

7. You forgot to upload `song4.mp3`! You are a bit lazy and know you just used a command to navigate inside the `songs` directory. Use the up arrow multiple times to see your most recently used commands. Can you retrieve the command you used to navigate inside the `songs` directory? Once you have, press enter to use it. Handy, right? 

8. You are now inside the `songs` directory, so create the file `song4.mp3` here. (Use the up arrow again to save time!)

9. Now, we need to add lyrics for the artists who tend to be a bit forgetful. Create a directory inside the `songs` directory called `lyrics` and navigate inside it, then create the file `lyrics.txt`. 

10. Ok, but now you need to go back to the set list and add song 4! The lazyness continues: you know the set list file is in the directory you were just in previously, so use `cd -` to navigate to the **previous** (NOT parent!) directory. 

11. **Reflect:** Do you understand the difference here between the **previous** directory and the **parent** directory? Make sure you can explain this difference to your neighbors before moving on! 

12. You want to add the name of song 4 to the list of songs inside the set list file. Add the song name "Party Rock Anthem" to the last line of the set list file, making sure to save the conents. 

**Tip:** You can use the nano editor here again. 

**Challenge:** See if you can add the song name to the file with one line in the command line using `echo` and output redirection (Make sure to use `>>`, the append operator!). 

13. You realize you don't like song 2 and want to remove it. Use `rm` to delete `song2.mp3` inside the `songs` directory. You are too lazy to move inside the `songs` directory again, so use **relative paths** here (and remember that using tab autocomplete can help you continue to be lazy and save effort typing)! 
**Hint:** I can remove a file inside directory B while being inside its parent directory A by typing the command `rm B/new_file`. 

14. **Reflect:** Were you checking your work with `ls` along the way? It's always a good idea to do so periodically, especially when modifying files/directories! 

-----

## Part 3: Discovering Commands (Help and Man Pages)

Knowing how to find documentation is often more valuable than memorizing every option.

### Exercise 3.1: Command Built-In Help (`--help` flag)

Many bash commands have a help page built-in via the `--help` (often shortened to `-h`) flag. 

1. Use the `--help` flag after the command `grep`. What information does this output tell you? Is it a comprehensive explanation of what the command actually does? 
2. Now, try using the `--help` flag after the command `rm`. What is different about this output? 
The `--help` flag is an optional addition to a command, and thus not all commands have a `--help` flag! It's a quick way to see an overview of the flag usage of a command, given the command supports that output. 

### Exercise 3.2: External Command Documentation (`man`)

How do we then get comprehensive information about what `grep` and `rm` do? Executable applications (like `ls`, `rm`, or `grep`) use the `man` (manual) pages.

1.  View the manual page for the `ls` command:
    ```bash
    man ls
    ```
2.  Scroll down and locate the descriptions for the `-l` and `-a` options. (Press `q` to quit the manual page viewer).
3.  **Challenge:** Use the `man` page to find out what the `grep` command actually does.

**Note:** The `man` command may not work if you are working inside a Git Bash terminal. This is because while it provides a simple Linux based terminal, it's not a full replicate. If you'd like to work inside an actual Linux terminal on a Windows, I suggest taking the time to install a WSL (Windows Subsystem for Linux) instead. 

-----

## Part 4: File Permissions and Ownership

Understanding file permissions is critical for security and script execution.

### Exercise 4.1: Interpreting `ls -la` Output

## Understanding and Changing File Permissions

The command line gives you fine-grained control over who can **read**, **write**, and **execute** your files. This control is managed by **permissions**.

### Exercise 4.1: Decoding File Permissions (`ls -la`)

1.  Run the **long listing** command:
    ```bash
    ls -la
    ```
2.  **Focus on the very first column** of the output. This 10-character string tells you everything about the file's permissions and type.

| Character Position | Meaning | Example |
| :---: | :--- | :---: |
| **1** | **File Type** | **d** (directory), **-** (file), or **l** (link) |
| **2-4** | **Owner/User** Permissions | **rwx** (Read, Write, Execute) |
| **5-7** | **Group** Permissions | **r-x** (Read, Execute, no Write) |
| **8-10** | **Other/World** Permissions | **r--** (Read only) |

The permission characters are:

  * **r** = **Read** (view file contents, list directory contents)
  * **w** = **Write** (modify or delete the file, create/delete files in a directory)
  * **x** = **Execute** (run the file as a program, enter a directory)
  * **-** = Permission denied

<!-- end list -->

3.  **Decode:** Look at the permissions for the `setlist.txt` file. For example, if you see:

    $$\text{-rw-r--r--}$$

      * The **User** (owner) has: **r w -** (Read and Write).
      * The **Group** has: **r - -** (Read only).
      * The **Other** has: **r - -** (Read only).

4.  **Identify:** What are the permissions for the `setlist.txt` file on your system (read as three groups of `rwx`)?

-----

### Exercise 4.2: Changing Permissions with Symbolic Mode (`chmod`)

The **`chmod`** (change mode) command is used to alter file permissions. We'll use **Symbolic Mode**, which uses intuitive characters to specify changes.

The syntax is: `chmod WHO OPERATION PERMISSION FILE`

| WHO | OPERATION | PERMISSION |
| :---: | :---: | :---: |
| **u** (User/Owner) | **+** (Add permission) | **r** (Read) |
| **g** (Group) | **-** (Remove permission) | **w** (Write) |
| **o** (Other/World) | **=** (Set permission exactly) | **x** (Execute) |
| **a** (All: u, g, and o) | | |

1.  Create a dummy script file:

    ```bash
    touch test_script.sh
    ```

2.  Run `ls -l test_script.sh` to see its default permissions (likely `-rw-rw-r--`).

3.  **Remove all write permissions for the group and others:**

    ```bash
    chmod go-w test_script.sh
    ```

      * **go**: affects the **G**roup and **O**ther.
      * **-**: **removes** the following permission.
      * **w**: the **Write** permission.

4.  **Grant executable permission only to the user (owner):** You want to affect the **user** (`u`), **add** (`+`) the **execute** (`x`) permission.

    ```bash
    # Type the command here:
    chmod u+x test_script.sh
    ```

5.  Run `ls -l test_script.sh` and verify the permissions string. It should now start with `-rwx` for the owner, and the permissions for group and others should be `-r--r--` (or something close to this, with no write permissions).

      * If you started with `-rw-rw-r--`, your final permissions should be: **`-rwx r-- r--`** (or just `-rwxr--r--`).

## Bonus Challenges 

### Exercise 4.3: Changing Permissions with Octal Mode (`chmod`)

Octal (numeric) mode is faster and sets the entire permission triplet at once using three digits (one for User, one for Group, one for Other).

| Permission | Binary | Octal |
| :--------- | :----- | :---- |
| read (r) | 100 | 4 |
| write (w) | 010 | 2 |
| execute (x) | 001 | 1 |

Permissions are summed: `rwx` = $4+2+1=7$. `rw-` = $4+2+0=6$. `r--` = $4+0+0=4$.

1.  Use octal mode to set the permissions of `test_script.sh` to:
      * **User:** `rwx` (7)
      * **Group:** `rx` (5)
      * **Other:** `r` (4)
    <!-- end list -->
    ```bash
    chmod 754 test_script.sh
    ```
2.  Run `ls -l test_script.sh` and verify the permissions string is now `-rwx r-x r--`.
3.  **Challenge:** What octal code would you use to grant read and write permission to *everyone* (User, Group, Other), but *no* execute permission?

-----

## Bonus Part 5: Types of Commands

### Exercise 5.1: Aliases for Shortcuts

Aliases provide a simple way to create shortcuts for longer commands.

1.  Define an alias named `lsl` that executes the command `ls -lh`.
2.  Use your new `lsl` alias in your workshop directory.
3.  **Cleanup:** Remove the alias using the `unalias` command.

### Exercise 5.2: Builtins, Executables, and the `type` Command

Bash must determine what kind of command it is executing. The `type` command provides this information.

1.  Use the `type` command to determine the command type for:
      * `cd`
      * `ls`
      * `alias`
2.  **Reflect:** Which of these are shell builtins (handled directly by Bash without creating a new process)? Which are executables (external programs usually found in your `PATH`)?

### Exercise 5.3: Keywords and Redirection Differences

Keywords like `[[` are part of Bash syntax and are parsed differently than builtins like `[`.

1.  Run the following command to compare two strings lexicographically using the `[` builtin:
    ```bash
    [ "a" < "b" ]
    ```
    *(Note: You will likely see an error message.*)
2.  Run the comparison again using the `[[` keyword:
    ```bash
    [[ "a" < "b" ]]
    ```
    *(Note: This command runs silently if true, with an exit status of 0.)*
3.  **Explain:** Why does the first command fail with an error about a file not being found, while the second one executes correctly for comparison?