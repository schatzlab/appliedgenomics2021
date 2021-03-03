## Assignment 5: BWT and RNA-seq
Assignment Date: Wednesday, Mar. 3, 2021 <br>
Due Date: Wednesday, Mar. 17 , 2021 @ 11:59pm <br>

### Assignment Overview

In this assignment you will write a simple BWT encoder and decoder, and explore a couple of aspects of RNA-seq (with a small introduction to clustering). For this assignment, you will have to generate some visualizations - we recommend R or Python, but use a language you are comfortable with! 

 **Make sure to show your work/code in your writeup!**

As a reminder, any questions about the assignment should be posted to [Piazza](https://piazza.com/class/kkbggatvarnj0).

### Question 1. BWT Encoding [10 pts]

In the language of your choice, implement a BWT encoder and encode the string below. Linear time methods exist for computing the BWT, although for this assignment you can use the simple method based on standard sorting techniques. Your solution does *not* need to be an optimal algorithm and can use O(n^2) space and O(n^2 lg n) time. 

Here is the recommended pseudo code (make sure to submit your code as well as the encoded string):

```
computeBWT(string s)
  ## add the magic end-of-string character
  s = s + "$"
 
  ## build up the BWM from the cyclic permutations
  ## note the ith cyclic permutation is just "s[i..n] + s[0..i]"
  StringList rows = []
  for (i = 0; i < length(s); i++)
    rows.append(cyclic_permutation(s, i))

  ## just use the builtin sort command
  sort(rows)

  ## now extract the last column
  string bwt = ""
  for (i = 0; i < length(s); i++)
    bwt += substr(rows[i], length(s),1)
  return bwt
```

String to encode:
```
I_am_fully_convinced_that_species_are_not_immutable;_but_that_those_belonging_to_what_are_called_the_same_genera_are_lineal_descendants_of_some_other_and_generally_extinct_species,_in_the_same_manner_as_the_acknowledged_varieties_of_any_one_species_are_the_descendants_of_that_species._Furthermore,_I_am_convinced_that_natural_selection_has_been_the_most_important,_but_not_the_exclusive,_means_of_modification.
```


### Question 2. BWT Decoder [10 pts]

In the language of your choice, implement a BWT decoder and decode the string below. 

One of the essential properties of the BWT is that it can be decoded back into the source text without any other additional information. This is accomplished by iteratively applying the Last-First property starting with the first character of the BWT until reaching the end of string character `'$'`. The Last-First property states there is an equivalence between the ith occurrence of a character in the first column and the ith occurrence of that character in the last column. This equivalence can be evaluated by counting how many occurrences of a character are present in the BWT string (the last column of the BWM) or by counting characters in the first column (which you will have to determine from the BWT itself). Again, faster methods exist (the FM-index) to determine the rank of each character but you can just count it explicitly here.

The pseudocode for decoding the string is as follows:

```
decodeBWT(String bwt) 
  String firstCol = makeFirstColumn(bwt)
  String text = ""
  
  ## By construction, '$' always starts the zeroth row
  row = 0;
  while (bwt.charAt(row) != '$')
      text.append(bwt.charAt(row));
      row = applyLF(firstCol, bwt.charAt(row), rank(bwt, row));
  
  return reverse(text)
```

String to decode:
```
.uspe_gexr_______$..,e.orrs,sdddeedkdsuoden-tf,tyewtktttt,sewteb_ce__ww__h_PPsm_u_naseueeennnrrlmwwhWcrskkmHwhttv_no_nnwttzKt_l_ocoo_be___aaaooaAakiiooett_oooi_sslllfyyD__uouuueceetenagan___rru_aasanIiatt__c__saacooor_ootjeae______ir__a
```

Hint: use your sourcecode from Q1 to debug Q2. Also start with simple strings like GATTACA or your own name.

#### Question 3. Time Series [20 pts]

[This file](http://schatz-lab.org/teaching/exercises/rnaseq/rnaseq.1.expression/expression.txt) contains normalized expression
values for 100 genes over 10 time points. Most genes have a stable background expression level, but some special genes show increased
expression over the timecourse and some show decreased expression.

- Question 3a. Cluster the genes using an algorithm of your choice. Which genes show increasing expression and which genes show decreasing expression,
and how did you determine this? What is the background expression level (numerical value) and how did you determine this?
[Hint: K-means and hierarchical clustering are common clustering algorithms you could try.]

- Question 3b. Calculate the first two principal components of the expression matrix. Show the plot and color the points based on their cluster from part (a). Does the PC1 axis, PC2 axis, neither, or both correspond to the clustering?

- Question 3c. Create a heatmap of the expression matrix. Order the genes by cluster, but keep the time points in numerical order.

- Question 3d. Visualize the expression data using t-SNE.

- Question 3e. Using the same data, visualize the expression data using UMAP.

- Question 3f. In a few sentences, compare and contrast the (1) heatmap, (2) PCA, (3) t-SNE and (4) UMAP results. Be sure to comment on understandability, relative positioning of clusters,
  runtime, and any other significant factors that you see.


#### Question 4. Sampling Simulation [10 pts]

A typical human cell has ~250,000 transcripts, and a typical bulk RNA-seq experiment may involve millions of cells. Consequently
in an RNAseq experiment you may start with trillions of RNA molecules, although your sequencer will only give a few million to billions of reads. 
Therefore your RNAseq experiment will be a small sampling of the full composition. We hope the sequences will be a representative
sample of the total population, but if your sample is very unlucky or biased it may not represent the true distribution. We will explore
this concept by sampling a small subset of transcripts (500 to 50000) out of a much larger set (1M) so that you can evaluate this bias.

In [data1.txt](data1.txt) with 1,000,000 lines we provide an abstraction of RNA-seq data where normalization has been performed and 
the number of times a gene name occurs corresponds to the number of transcripts in the sample.

Question 4a. Randomly sample 500 rows. Do this simulation 10 times and record the relative abundance of each of the 15 genes. Make a scatterplot the mean vs. variance of each gene (x-axis=mean of gene_i, y-axis=variance of gene_i)

Question 4b. Do the same sampling experiment but sample 5000 rows each time. Again plot the mean vs. variance.

Question 4c. Do the same sampling experiment but sample 50000 rows each time. Again plot the mean vs. variance.

Question 4d. Is the variance greater in (a), (b) or (c)? What is the relationship between mean abundance and variance? Why?


#### Question 5. Differential Expression [20 pts]

Question 5a. Using the file from question 4 (data1.txt) along with [data2.txt](data2.txt), randomly sample 500 rows from each file. 
Sample 5 times for each file (this emulates making experimental replicates) and conduct a paired t-test for 
differential expression of each of the 15 genes. Which genes are significantly differentially expressed at the 0.05 level and what is their mean fold change?

Question 5b. Make a volano plot of the data: x-axis=log2(fold change of the mean expression of gene_i); y-axis=-log_10(p_value comparing the expression of gene_i). Label all of the genes that show a statistically siginificant change

Question 5c. Now sample 5000 rows 10 times from each file, equivalent to making more replicates. Which genes are now significant at the 0.05 level and what is their mean fold change?

Question 5d. Make a volcano plot using the results from 5c (label any statistically significant genes)

Question 5e. Perform the simulations from parts a/c but sample 50000 rows each time from each file. Which genes are significant and what is their mean fold change? 

Question 5f. Make a volcano plot from 5e (label any statistically significant genes)

Question 5g. Now examine the complete files: compare the fold change in the complete files vs the different subsamples. Address replicates and the size of the random sample. If you want, you can perform additional simple simulation experiments with this data - describe what you did and how it informed your answer to this question.


### Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and all relevant figures (as needed). Make sure to clearly label each of the subproblems and give the exact commands and/or code snippets you used for solving the question. You do not need to show code for plotting. Submit your solutions by uploading the PDF to [GradeScope](https://www.gradescope.com/courses/236625), and remember to select where in your submission each question/subquestion is.

If you submit after this time, you will start to use up your late days. Remember, you are only allowed 96 hours (4 days) for the entire semester!
