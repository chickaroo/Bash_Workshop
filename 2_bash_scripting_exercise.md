# Bash Scripting Exercise

In this section, we will use bash scripts to automating a common task: downloading and analyzing protein sequences.

## Building a Protein FASTA Downloader

### Part 1: Create and Initialize the Script

Create and open a new file named `prot_seq_tool.sh` using your text editor in the command line:

Add the Shebang: The very first line of any Bash script is the Shebang (`#!`). It tells your operating system which program to use to execute the rest of the file (in our case, the bash shell). This line is mandatory for a script to run correctly.

Add this line to the very top of `prot_seq_tool.sh`:

```bash
#!/usr/bin/env bash
```

We need to make sure our script is executable, which means that we can run the script. To do this, save and exit the editor, then change the permissions of the script file so that the user can execute the file: `chmod u+x prot_seq_tool.sh`


### Part 2: Accepting Input and Defining Variables

We want our script to be flexible: it should work for any protein ID we give it. We do this by accepting command-line arguments.

**Variables:** In Bash, variables are denoted with the `$` symbol. For example, we can have a simple script that prints the value of a variable: 

```bash
#!/usr/bin/env bash

VAR1="Comp Bio Soc"

echo $VAR1
```
**Note:** there are no spaces when declaring variables! Bash syntax does not accept `VAR1 = "Comp Bio Soc"`. 

We can embedd our variables within strings to use them flexibly with `{}` operators. For example, 

```bash
#!/usr/bin/env bash

VAR1="Comp Bio Soc"

echo "Welcome to ${VAR1}s workshop"
```

**Test:** Save the above code in your script and try to run the script by using the bash command: `bash prot_seq_tool.sh`. Try to run the script again after removing the `{}` operators. Why is it important to use these operators? 

### Part 3: Arguments 

Define Variables: In Bash, arguments passed when running the script are stored automatically in variables like $1 (first argument), $2 (second argument), etc. We will use the first argument ($1) for our protein ID.

For example, you can define variables as the arguments of a script like this: 

```bash
#!/usr/bin/env bash

VAR1="$1"
VAR2="$2"
```

Use this example to define the variable `PROTEIN_ID` as the first argument your script accepts. 

### Part 4: Download the FASTA file from UniProt

We can use the command `wget` to download a file from the internet and sive it to your local machine. If you'd like, you can use `man` to see a more detailed description of what `wget` does. 

The URL to download e.g. the protein sequence for human hemoglobin subunit beta is https://rest.uniprot.org/uniprotkb/P68871.fasta. 

**Do it yourself:** Write a bash command in your script using `wget` to download any given protein from Uniprot. Remember, we can embed variables in a string using the `"Welcome to ${VAR1}s workshop"` syntax. 


**Test the Download:** Run the script with the human P53 tumor suppressor protein ID (P04637):

```bash
bash prot_seq_tool.sh P04637
```

Check your work with `ls`! A file called P04637.fasta should now be in your directory.

If you want, you can inspect the contents of this FASTA file using commands like `cat` or `head`. 

### Part 5: Amino Acid Composition

Now it's starting to get more complex! We want to read the downloaded FASTA file and automatically output some key aspects our sequence, like the sequence length. 

First, let's introduce some Bash tools that you may need in the following exercises. 

**While loop:**

``` bash

counter=1

while [[ $counter -le 5 ]]; do
    echo "Count: $counter"
    ((counter++))
done

```

`while [[ condition ]]` checks if the condition is true
`do` marks the start of the code that repeats
The code inside runs over and over as long as the condition is true
`done` marks the end of the loop
`-le` means "less than or equal to"
`((counter++))` adds 1 to counter

Use a while loop to read a file line by line: 

``` bash
while read -r line; do
    echo "Line: $line"
done < filename.txt
```

Can you find out what the `-r` does? 

**If-Statements:**

``` bash

if [[ condition ]]; then
    # code if true
else
    # code if false
fi

```

Hint: `[[ $line == ">"* ]]` checks if a line starts with the character ">". 


**Length of a string:**

``` bash

string_length=${#my_string}

```
**For-loop:**

``` bash
for (( i=0; i<10; i++ )); do
    echo $i
done
```

**Simple Arrays:**

``` bash
fruits=("apple" "banana" "cherry") # Method 1: create with values

# Method 2: Create empty and add items
animals=()
animals[0]="cat"
animals[1]="dog"
animals[2]="bird"

echo ${fruits[0]}    # Prints the 0th element of the array: "apple"
echo ${#fruits[@]}    # Prints the length of the array: "3"

# loop through the array
for (( i=0; i<${#fruits[@]}; i++ )); do
    echo "${fruits[$i]}"
done

# for-each loop
for fruit in "${fruits[@]}"; do
    echo "$fruit"
done

```


### Exercise 5.1: 

1. Print only the header of the FASTA file. 
2. Print the length of the sequence. Make sure your outputs are understandable, like `sequence_length: 11`
3. Add another argument to accept a specific amino acid character and output how many times that amino acid occurs in the sequence. 
4. **Challenge:** Output the amino acid composition of the sequence, i.e. the number of occurences of each amino acid in the sequence. Think about using arrays; you may have to use more than one! 

**Note:** We have not covered more detailed elements of bash scripts like error handling and debugging output. If you'd like, extend your script to handle inputs that aren't in the expected format. 

**Next Note:** Bash was never intended to be a complex programming language, rather it is there to help you automate command line workflows. If you find yourself coding complex logical algorithms in Bash, it's probably time to switch to a higher level language like Python. 

### Optional Part 6: Explore an Alternative Solution to Amino Acid Composition using Bash Commands and the Pipe (`|`)

Instead of using complex loops, we will use a series of commands connected by the pipe symbol (|). This is fast and powerful, and can be simpler to use if you understand the commands well. 

If you want to try to solve this yourself, do not scroll below this line! I've provided a solution and a breakdown of what each command is doing below. 

Hint: You'll need commands we haven't used before here. Google is your friend! 


------------



``` bash
echo ""
echo "--- Amino Acid Composition (Pipeline Method) ---"

# 1. Use 'grep -v' to filter out the header line (starts with '>')
# 2. Use 'tr -d' to remove all newline characters (creating one long string)
SEQUENCE=$(grep -v '>' "${OUTPUT_FILE}" | tr -d '\n')

# 3. Process the sequence for counting:
echo "$SEQUENCE" | \
fold -w 1 | \
sort | \
uniq -c | \
awk '{print $2 ": " $1}'
```

What's happening in the pipeline?

`echo "$SEQUENCE" |`: Takes the long protein string and passes it to the next command.

`fold -w 1 |`: Splits the string, putting each character on a new line.

`sort |`: Puts all the A's together, C's together, etc.

`uniq -c |`: Counts how many consecutive identical lines (characters) there are.

`awk '{print $2 ": " $1}'`: Formats the final output nicely.

Well that is a nice and short script, right? Being familiar with Bash commands can indeed make your life that much easier. 


TODO: 

Add How to Install WSL for Windows
Add Intro to HPC Resources