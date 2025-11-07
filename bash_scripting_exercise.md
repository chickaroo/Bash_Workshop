# Bash Scripting Exercise

# WIP!!!

This section focuses on writing self-contained shell scripts and introducing fundamental programming constructs.

### Exercise 4.1: Script Setup and Data Download

Every script needs a shebang line and executable permission. We will also use the `wget` command, an executable, to download external data.

1.  Create a new script file named `fasta_processor.sh`.
2.  Place the recommended shebang at the top:
    ```bash
    #!/usr/bin/env bash
    ```
3.  Inside the script, add the following lines to define the URL and download the data:
    ```bash
    # Variable holding the URL for a small FASTA protein sequence file (P0DPF8)
    FASTA_URL="https://www.uniprot.org/uniprot/P0DPF8.fasta"
    # Use wget to download the file into the current directory
    wget -q "$FASTA_URL" -O protein_data.fasta
    ```
4.  Save the script. Give it executable permission: `chmod +x fasta_processor.sh`.
5.  Execute the script (`./fasta_processor.sh`) and confirm that a file named `protein_data.fasta` was created silently.

### Exercise 4.2: Positional Parameters and Argument Checking

Positional parameters (`$1`, `$2`, etc.) hold the arguments passed to your script. `$#` holds the total number of arguments.

1.  Modify `fasta_processor.sh` to check if the user provided *exactly one* argument (which will be the line number to print). Place this logic **before** the `wget` command.

2.  Add a check using an `if` statement for error handling and a usage message:

    ```bash
    # Check if the number of arguments ($#) is not equal to 1
    if [[ $# -ne 1 ]]; then
      echo "Error: Please provide exactly one argument (the line number)." >&2
      echo "Usage: $0 <line_number>" >&2 # $0 is the script's name
      exit 1
    fi

    # ... rest of the script (wget command) ...
    ```

3.  Run the script with:

      * No arguments (`./fasta_processor.sh`).
      * Two arguments (`./fasta_processor.sh 1 2`).
      * One argument (`./fasta_processor.sh 2`). (It should now continue past the check).

### Exercise 4.3: Processing Data with a `for` Loop

The `for` loop is ideal for iterating over a list of items.

1.  **Challenge:** Use a `for` loop to iterate over the contents of `protein_data.fasta` and print only the header line (which starts with `>`).

2.  Inside your `fasta_processor.sh` script, add this *incorrect but common* loop structure **after** the `wget` command:

    ```bash
    echo "--- Processing with simple for loop (Vulnerable to Word Splitting) ---"

    # NOTE: This is a poor pattern for reading files, as it splits lines on ALL
    # whitespace, not just newlines. If a line had a space, it would be treated
    # as multiple items.
    for line in $(cat protein_data.fasta); do
      if [[ "$line" == ">"* ]]; then
        echo "HEADER FOUND: $line"
      fi
    done
    ```

3.  Execute the script with one argument (`./fasta_processor.sh 2`).

4.  **Observe:** Did the header print correctly? Look at the sequence lines—if they contained spaces, they would be split and processed as separate "lines," highlighting a fundamental flaw of this `for` loop structure for file processing.

### Exercise 4.4: Robust Processing with a `while` Loop

The `while read` loop is the standard, robust method for processing a file line-by-line, as it correctly handles spaces within lines.

1.  Comment out the previous `for` loop block in your script.

2.  Replace it with the following robust `while` loop structure:

    ```bash
    echo "--- Processing with robust while loop (Correct Line Reading) ---"

    # The IFS= ensures internal field separator (splitting) only happens on
    # newlines, not spaces.
    # The read -r prevents backslashes from being interpreted (Raw input).
    LINE_COUNT=0
    TARGET_LINE="$1" # Use the positional parameter passed to the script

    while IFS= read -r line; do
      # Increment the counter
      LINE_COUNT=$((LINE_COUNT + 1))

      # Use an if statement to check if the current line number matches the target
      if [[ $LINE_COUNT -eq $TARGET_LINE ]]; then
        echo "Target Line ($TARGET_LINE) Content: $line"
        break # Stop reading once the line is found
      fi

    done < protein_data.fasta # Pipe the file content into the loop
    ```

3.  Execute the script, targeting the second line (which is usually the start of the sequence): `./fasta_processor.sh 2`.

4.  **Reflect:** The `while IFS= read -r line` pattern prevents word splitting and backslash interpretation. Why are these protections (`IFS=` and `-r`) critical for reliable file processing in Bash?

### Exercise 4.5: Cleaning Up with Conditional Logic

It's good practice to clean up temporary files created by a script.

1.  Add a final `if` statement to your `fasta_processor.sh` script to check if the file `protein_data.fasta` exists, and if it does, delete it.
    ```bash
    # Cleanup section
    if [[ -f protein_data.fasta ]]; then
      rm protein_data.fasta
      echo "Cleanup successful."
    fi
    ```
2.  Run the complete script one last time with a valid argument (`./fasta_processor.sh 3`).
3.  **Confirm:** The script should execute, print the usage message if no argument is given, download the file, process the third line, and then delete the file before exiting.
4.  Run `ls` to ensure the file is gone.

-----

That concludes the restructured workshop guide\! Let me know if you'd like to dive deeper into any of these concepts, like writing functions or handling command-line options.

http://googleusercontent.com/immersive_entry_chip/0

I'm glad you liked the direction\! This new, expanded Part 4 should give you excellent practice with essential Bash scripting control flow and best practices for file handling. Let me know if you would like to explore functions or more complex regular expressions next\!