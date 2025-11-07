# Commmand Line Exercise

Working in the command line can seem daunting at first, but these exercises are designed to get you comfortable with the environment. You'll only get better if you practice and spend time with it! 

Work through these exercises in your own command line. If you want, you can make a separate file to note down things you learn or any questions you have.

-----

## Part 1: Commands and Arguments

### Exercise 1.1: Basic Command Execution and Whitespace

The shell separates commands and arguments based on whitespace.

1.  Create a directory named `bash_workshop` and navigate into it. (Make sure you understand where this directory is within your general directory structure!)
2. Move inside this directory using the `cd` command. 
3.  Run the `ls` command to observe the initial directory state.
4.  Use the `touch` command to create three files named `alvin`, `theodor`, and `simon` in a single command, ensuring there are different amounts of space (one, two, or more) between the arguments.
5.  Run `ls` again to confirm the files were created correctly.
6.  **Reflect:** Did the varying amount of whitespace between the filenames affect how `touch` interpreted the arguments?

### Exercise 1.2: Globbing and Argument Separation

A **glob** (like `*`) is a pattern that the shell expands into a list of filenames before the command executes.

1.  Use a single `rm` command with a glob to delete all files in your current directory.
2. List the contents of your directory to see what `rm` did.


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
2.  **Dangerous Test:** Attempt to delete only `My Important File.txt` **without** surrounding the filename in quotes.
3.  Run `ls` to see which files remain.
4.  **Fix:** Now, delete the remaining file correctly by using **double quotes** around its filename.
5. **Reflect:** How should we deal with files containing whitespaces? Do you think naming files with whitespaces is a good idea when working in the command line? 

-----

## Part 2: Strings

### Exercise 2.1: Strings in Command Execution

In Bash, almost everything is treated as a string.

1.  Create a text file named `set_list` using an editor with the following content (on separate lines):

    ```text
    You Spin Me Round
    Uptown Funk
    The Chipmunk Song
    ```

**Tip:** use nano, a simple editor built in to your command line. 

**Challenge:** use Vim as your editor instead! 

2.  Run the command `cat set_list`.

3.  **Reflect:**

      * We typed a command: `cat set_list`. The shell reads this command as a string, and then divides it into the substrings `cat` and `set_list`. As far as the shell is concerned, `set_list` has no meaning, it's just a string with eight characters in it. `cat` receives the argument `set_list`, which is a string of a filename. The string `set_list` has become meaningful because of how it was used.

      * The file happens to contain some text, which we see on our terminal. The entire file content — taken as a whole — is a string, but that string is not meaningful. However, if we divide the file into lines (and therefore treat each line as a separate string), then we see each individual line has meaning.

      * We can divide the final line into words, but these words are not meaningful by themselves. We don't know the song "Chipmunk". Dividing the lines into words is not a useful thing to do in this example. But the shell doesn't know any of this — only we do!

4. Let's practice moving around in the command line efficiently with strings: 
    * Make a new directory called `songs` and navigate instide it. 
    * Create the files `song1.mp3` `song2.mp3` `lyrics1.txt` `lyrics2.txt`. You can do this all in one line!
    * You want to send `song1.mp3` to a friend but forgot where the file is to attach to an email. Use `pwd` to help see where you are. 
    * Use `cd ..` to navigate back to your parent directory. 
    * You realize you hate song 2 and want to remove it. Use `rm` to delete `song2.mp3` and `lyrics2.txt` inside the `songs` directory. Use relative paths here, and remember that using tab autocomplete will make your life much easier! 
    * Check your work with `ls`. 

-----

## Part 3: Discovering Commands (Help and Man Pages)

Knowing how to find documentation is often more valuable than memorizing every option.

### Exercise 3.1: Internal Command Documentation (`help`)

Many Bash builtins have their own internal documentation accessible via the `help` command.

1.  Use the `help` command on the `type` builtin:
    ```bash
    help type
    ```
2.  Use the `help` command on the `for` keyword (try to locate the structure for a simple `for` loop).
3.  **Contrast:** Now try to run `help ls`. What is the output, and why did this command fail to provide help documentation?

### Exercise 3.2: External Command Documentation (`man`)

Executable applications (like `ls` or `grep`) use the `man` (manual) pages.

1.  View the manual page for the `ls` command:
    ```bash
    man ls
    ```
2.  Scroll down and locate the descriptions for the `-l` and `-a` options. (Press `q` to quit the manual page viewer).
3.  **Challenge:** Use the `man` page to find out which command is used to display the contents of a file (like `cat` or `less`).

-----

## Part 4: File Permissions and Ownership

Understanding file permissions is critical for security and script execution.

### Exercise 4.1: Interpreting `ls -la` Output

The command `ls -la` (long listing, all files) provides detailed information about files, including permissions.

1.  Run `ls -la` in your `bash_workshop` directory. Focus on the very first column of the output.
2.  **Decode:** This 10-character string represents the file type and permissions.
      * The first character (`-`, `d`, or `l`) is the file **type** (`-` for file, `d` for directory, `l` for link).
      * The next nine characters are permission triplets: **User** (owner), **Group**, and **Other** (everyone else).
3.  **Identify:** What are the permissions for the `set_list` file (read as three groups of `rwx`)?

### Exercise 4.2: Changing Permissions with Symbolic Mode (`chmod`)

Symbolic mode uses characters to specify *who* (`u`=user, `g`=group, `o`=other, `a`=all) gets *what* permission (`+`=add, `-`=remove, `=`=set) for *which* permission type (`r`, `w`, `x`).

1.  Create a dummy script file: `touch test_script.sh`.
2.  Remove all write permissions for the group and others:
    ```bash
    chmod go-w test_script.sh
    ```
3.  Grant executable permission only to the user (owner), using the information above to figure out the correct symbols.  

4.  Run `ls -l test_script.sh` and verify the permissions string matches `-rwx r-- ---`. (The group/other read permissions might vary, but the `u+x` should be present.)

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