## Assignment 3: Coverage, Genome Assembly, and Variant Calling
Assignment Date: Wednesday, Feb. 10, 2020 <br>
Due Date: Wednesday, Feb. 17, 2020 @ 11:59pm <br>

### Assignment Overview

In this assignment you will take a closer look at coverage, build and analyze a simple de Bruijn graph, and write your own compacted de Bruijn graph generator that you will test on a small microbial genome.

As a reminder, any questions about the assignment should be posted to [Piazza](https://piazza.com/class/kkbggatvarnj0).

### Question 1. Coverage simulator [20 pts]

- Q1a. How many 100bp reads are needed to sequence a 1Mbp genome to 5x coverage?

- Q1b. In the language of your choice, simulate sequencing 5x coverage of a 1Mbp genome with 100bp reads and plot the histogram of coverage. Note you do not need to actually output the sequences of the reads, you can just randomly sample positions in the genome and record the coverage. You do not need to consider the strand of each read. The start position of each read should have a uniform random probabilty at each possible starting position (1 through 999,901). You can record the coverage in an array of 1M positions. Overlay the histogram with a Poisson distribution with lambda=5

- Q1c. Using the histogram from 1b, how much of the genome has not been sequenced (has 0x coverage)? How well does this match Poisson expectations?

- Q1d. Now repeat the analysis with 15x coverage: 1. simulate the appropriate number of reads, 2. make a histogram, 3. overlay a Poisson distribution with lambda=15, 4. compute the number of bases with 0x coverage, and 5. evaluate how well it matches the Poisson expectation.


### Question 2. de Bruijn Graph construction [15 pts]
- Q2a. Draw (by hand or by code) the de Bruijn graph for the following reads using k=3 (assume all reads are from the forward strand, no sequencing errors, complete coverage of the genome)

```
ATTCA
ATTGA
CATTG
CTTAT
GATTG
TATTT
TCATT
TCTTA
TGATT
TTATT
TTCAT
TTCTT
TTGAT
```

- Q2b. Assume that the maximum number of occurrences of any 3-mer in the actual genome is 4 using the k-mers from Q2a. Write one possible genome sequence


- Q2c. What would it take to fully resolve the genome? [In a few sentences]


### Question 3. Compacted de Bruijn Graphs [25 pts]

For this question, you will have to create a simple compacted de Bruijn graph generator, and apply it to the Staphylococcus aureus reference genome to answer the questions below.

Download the Staphylococcus aureus reference genome here: https://github.com/schatzlab/appliedgenomics2021/raw/master/assignments/assignment3/Staphylococcus_aureus.fna.gz. The genome is about 2.8 Mbp in length, but you still should easily be able to process it on a laptop.

We have also provided a shorter sequence (of length 100,000 bp) that we have used to answer the questions below. You can use it to verify that your implementation is correct (by running it on this shorter sequence, and comparing your answers to ours), before answering the questions below about the complete Staphylococcus aureus genome. You can download this shorter sequence here: https://github.com/schatzlab/appliedgenomics2021/raw/master/assignments/assignment3/sample.fna.

For this question, please make sure to include your code in your submission so that we can give you partial credit if one of your answers is incorrect. 

- Q3a. Using k = 25, how many nodes are there in the simple de Bruijn graph generated from Staphylococcus aureus? How many edges are there? [Hint: Start by breaking the genome down into k-mers to determine all of your edges and nodes, and maintain some simple data structures (hash table, dictionary, etc) to tie them together - this is all you have to do to get a simple de Bruijn graph! Note you should construct a simple graph, with at most 1 edge between a pair of nodes, even if their sequences are repeated multiple times in the genome]

- Q3b. The out-degree of a node is the number of directed edges that start at the node, and the in-degree of a node is the number of directed edges that end at the node. Plot one histogram of the distribution of out-degrees in your de Bruijn graph, and another of the distribution of in-degrees in your de Bruijn graph. [Hint: Use the nodes and edges you identified in 3a, and get a count of how many nodes have out degree/in degree 0, 1, ..., n.]

- Q3c. Recall that an edge can be compacted if the node is starts from has out-degree = 1, and the node it ends at has in-degree = 1. In the de Bruijn graph of Staphylococcus aureus, how many such "compactable" edges are there?

- Q3d. Compact all of the edges that can be compacted. How many nodes and edges are there now? What is are the minimum and maximum lengths of a sequence that can be obtained from the de Bruijn graph? What is the N50 length?

- Q3e. Repeat question 3d for k = 50 and k = 100. Make sure to report number of nodes, number of edges, minimum sequence length, maximum sequence length, and N50 sequence length.


### Expected Output for sample.fna

Here are the answers that we expect when using sample.fna (instead of the Staphylococcus aureus reference genome) - please use this to verify the correctness of your code.

- 3a: Number of nodes = 99219, Number of edges = 99254.

- 3b:

| Out-Degree | # Nodes |
|------------|---------|
| 0          | 1       |
| 1          | 98558   |
| 2          | 571     |
| 3          | 81      |
| 4          | 8       |


| In-Degree | # Nodes |
|------------|---------|
| 0          | 1       |
| 1          | 98558   |
| 2          | 571     |
| 3          | 81      |
| 4          | 8       |

- 3c: Number of compactable edges = 98498.

- 3d and 3e:
	- k = 25: # Nodes = X, # Edges = X, Min Length = X, Max Length = X, N50 Length = X.
	- k = 50: # Nodes = X, # Edges = X, Min Length = X, Max Length = X, N50 Length = X.
	- k = 100: # Nodes = X, # Edges = X, Min Length = X, Max Length = X, N50 Length = X.


### Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and 
all relevant figures (as needed). Make sure to clearly label each of the subproblems and give the exact commands and/or code snippets you used for 
solving the question. You do not need to show code for plotting. Submit your solutions by uploading the PDF to [GradeScope](https://www.gradescope.com/courses/236625), and remember to select where in your submission each question/subquestion is.

If you submit after this time, you will start to use up your late days. Remember, you are only allowed 96 hours (4 days) for the entire semester!
