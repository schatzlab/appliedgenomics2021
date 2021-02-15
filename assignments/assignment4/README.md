## Assignment 4: Coverage, Genome Assembly, and de Bruijn Graphs
Assignment Date: Wednesday, Feb. 17, 2020 <br>
Due Date: Wednesday, Mar. 3 , 2020 @ 11:59pm <br>

Some of the tools you will need to use may only run in a linux or mac environment. 
If you do not have access to a linux/mac machine, download and install a virtual 
machine or ubuntu instance following the directions here: https://github.com/schatzlab/appliedgenomics2018/blob/master/assignments/virtualbox.md

Alternatively, you might also want to try out this docker instance that has these tools preinstalled: 
[https://github.com/mschatz/wga-essentials](https://github.com/mschatz/wga-essentials)

### Assignment Overview

In this assignment you will get some experience with small variant analysis, take a look at mappability, and analyze some variant data.

For questions 1, 3 and 4 of this assignment, you will be using chromosome 22 from build 38 of the human genome - download it here: [http://hgdownload.cse.ucsc.edu/goldenPath/hg38/chromosomes/chr22.fa.gz](http://hgdownload.cse.ucsc.edu/goldenPath/hg38/chromosomes/chr22.fa.gz). Whenever we refer to chromosome 22 in this assignment, this is what you should use.

As a reminder, any questions about the assignment should be posted to [Piazza](https://piazza.com/class/kkbggatvarnj0).

### Question 1. Small Variant Analysis [10 pts]

Download the read set from here:  
[http://schatzlab.cshl.edu/data/teaching/sample.tgz](http://schatzlab.cshl.edu/data/teaching/sample.tgz)

For this question, you may find this tutorial helpful:  
[http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html](http://clavius.bc.edu/~erik/CSHL-advanced-sequencing/freebayes-tutorial.html)

- 1a. Using bowtie2, how many reads align to the chromosome 22 reference? How many reads did not align? How many aligned reads had a mate that did not align (AKA singletons)? Count each read in a pair separately.  
[Hint: Build the index using `bowtie2-build`, align reads using `bowtie2`, analyze with `samtools flagstat`.]

- 1b. How many reads are mapped to the reverse strand? Count each read in a pair separately.   
[Hint: Find out what SAM flags mean [here](https://broadinstitute.github.io/picard/explain-flags.html) and use samtools view.]

- 1c. How many high-quality (QUAL > 20) single nucleotide and indel variants does the sample have? Of the indels, how many are insertions and how many are deletions?  
[Hint:  Identify variants using `freebayes` - sort the SAM file first. Then call variants with freebayes. Filter using `bcftools filter`, and summarize using `bcftools stats`.]


### Question 2. Binomial Distribution [10 pts]

- 2a. For coverage n = 10 to 200, calculate the maximum number of minor allele reads (round down) that would make your one-sided binomial test reject the null hypothesis p=0.5 at 0.05 significance. Plot coverage on the x-axis and (number of reads)/(coverage) on the y-axis. Note this is the minimum number of reads that are necessary to believe we might have a heterozygous variant on the second haplotype rather than just mere sequencing error.

- 2b. What asymptote does the plot seem to approach? Why is this?


### Question 3. Mappability Analysis [15 pts]

- 3a. Using k = 100, extract every k-mer from chromosome 22, and align them back to chromosome 22 using bowtie2. How many 100-mers map uniquely (i.e. map to just one position) in chromosome 22? How many map to multiple positions? Make a histogram of the number of k-mers that map to a given number of positions in the genome (x-axis = number of positions mapped to, y-axis = number of k-mers that map to this many positions).

- 3b. For each position in chromosome 22, count how many k-mers uniquely mapped to it. Make a histogram of the number of positions in chromosome 22 with a given number of k-mers uniquely mapping to them. Use k = 100, and the 100-mers you generated in 3a. [Hint: What is the maximum number of k-mers that can uniquely map to a single position? How many 100-mers can overlap one base in chromosome 22?]

- 3c. Repeat the previous two questions for k = 25, 50 and 500. How does number of positions a k-mer maps to change with different k? How does the number of k-mers that uniquely map to a given position change? Provide plots for each value of k, as well as a couple of sentences discussing the effect of k on both.


#### Question 4. De novo mutation analysis [20 pts]

For this question, we will be focusing on the de novo variants identified in this paper:<br>
[http://www.nature.com/articles/npjgenmed201627](http://www.nature.com/articles/npjgenmed201627)

Download the de novo variant positions from here (Supplementary Table S4):<br>
[http://www.nature.com/article-assets/npg/npjgenmed/2016/npjgenmed201627/extref/npjgenmed201627-s3.xlsx](http://www.nature.com/article-assets/npg/npjgenmed/2016/npjgenmed201627/extref/npjgenmed201627-s3.xlsx)

Download the gene annotation of the human genome here: <br>
[ftp://ftp.ensembl.org/pub/release-87/gff3/homo_sapiens/Homo_sapiens.GRCh38.87.gff3.gz](ftp://ftp.ensembl.org/pub/release-87/gff3/homo_sapiens/Homo_sapiens.GRCh38.87.gff3.gz)

Download the annotation of regulatory variants from here:<br>
[ftp://ftp.ensembl.org/pub/release-87/regulation/homo_sapiens/homo_sapiens.GRCh38.Regulatory_Build.regulatory_features.20161111.gff.gz](ftp://ftp.ensembl.org/pub/release-87/regulation/homo_sapiens/homo_sapiens.GRCh38.Regulatory_Build.regulatory_features.20161111.gff.gz)

**NOTE** The variants are reported using version 37 of the reference genome, but the annotation is for version 38. Fortunately, you can 'lift-over' the variants to the coordinates on the new reference genome using several avaible tools. I recommmend the [UCSC liftover tool](https://genome.ucsc.edu/cgi-bin/hgLiftOver) that can do this in batch by converting the variants into BED format. Note, some variants may not successfully lift over, especially if they become repetitive and/or missing in the new reference, so please make a note of how many variants fail liftover.

- 4a. How much of the genome is annotated as a gene?

- 4b. What is the sequence of the shortest gene on chromosome 22? [Hint: `bedtools getfasta`]

- 4c. How much of the genome is an annotated regulatory sequence (any type)? [Hint `bedtools merge`]

- 4d. How much of the genome is neither gene nor regulatory sequences [Hint: `bedtools merge` + `bedtools subtract`]

- 4e. Using the [UCSC liftover tool](https://genome.ucsc.edu/cgi-bin/hgLiftOver), how many of the variants can be successfully lifted over to hg38?

- 4f. How many variants are in genes? [Hint: convert xlsx to BED, then `bedtools`]

- 4g. How many variants are in *any* annotated regulatory regions? [Hint: `bedtools`]

- 4h. What type of annotated regulatory region has the most variants? [Hint: `bedtools`]

- 4i. Is this a statistically significant number of variants (P-value < 0.05)? [Hint: If you don't want to calculate this analytically, you can do an experiment. Try simulating the same number of variants as the original file 100 times, and see how many fall into this regulatory type. If at least this many variants fall into this feature type more than 5% of the trials, this is not statistically significant]


### Packaging

The solutions to the above questions should be submitted as a single PDF document that includes your name, email address, and 
all relevant figures (as needed). Make sure to clearly label each of the subproblems and give the exact commands and/or code snippets you used for 
solving the question. You do not need to show code for plotting. Submit your solutions by uploading the PDF to [GradeScope](https://www.gradescope.com/courses/236625), and remember to select where in your submission each question/subquestion is.

If you submit after this time, you will start to use up your late days. Remember, you are only allowed 96 hours (4 days) for the entire semester!

## Resources

#### [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/index.shtml) - Short read aligner

```
conda install bowtie2
bowtie2-build chr22.fa chr22
bowtie2 -x chr22 -1 sample/pair.1.fq -2 sample/pair.2.fq > sample.sam
```

While running alignments, if you get an error `Warning: Exhausted best-first chunk memory for read XXXX; skipping read` increase the command-line parameter `--chunkmbs`.

#### [FreeBayes](https://github.com/ekg/freebayes) - Small Variant Identification

```
conda install freebayes
freebayes -f chr22.fa sample.bam > sample.vcf
```

#### [bcftools](https://samtools.github.io/bcftools/bcftools.html) - VCF Summarry

```
conda install bcftools
bcftools filter -e "QUAL<20" sample.vcf > filtered.vcf
bcftools stats filtered.vcf > stats.txt
```


#### [BEDTools](http://bedtools.readthedocs.io/en/latest/) - Genome Arithmetic

Get bedtools from conda, if you haven't already.

```
conda install bedtools
```