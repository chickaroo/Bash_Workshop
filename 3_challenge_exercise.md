# Challenge Exercise

1. Download the DNA sequence for the hemoglobin subunit beta (Gene ID: 3043) from the NCBI website in your command line. To do this, you may want to install the NCBI Datasets command-line tools, or alternatively the Entrez Direct E-utilities. 
2. Write a bash script that determines the RNA complement of a given DNA sequence in a FASTA file format. Your script should take a FASTA file as input and output the RNA complement strand to the command line. 

Remember, given a DNA strand, its transcribed RNA strand is formed by replacing each nucleotide with its complement:

G -> C

C -> G

T -> A

A -> U


3. Alter your script so it writes the RNA complement output to a given output file.

4. If you have time, also calculate and output the percent GC content in the original DNA sequence. You can output this after the complementary RNA strand. 