# Project Ideas

Here are a few selected projects organized by theme, although you are also free to present your own project ideas. A good project is one that:
 
  1. Has a well defined goal
  2. Has a well defined method proposed for solving it; and 
  3. Has appropriate data and resources available. 
 
If any of these are not available, your project will not be successful, especially in the limited time remaining for class. A successful model for the class project is to apply a technique developed in a different context to the biological problem of your choice. Another successful model is to identify an important paper of interest and then try to improve apon their method in some way (faster, less memory, more sensitive, more precise, novel species, novel data sets, etc).


## Basecalling and signal processing

1. Develop an improved base calling algorithm (potentially modification aware) for Oxford Nanopore or PacBio sequencing using recurrent neural networks or other ML approach:
[Nanocall](https://academic.oup.com/bioinformatics/article/33/1/49/2525680/Nanocall-an-open-source-basecaller-for-Oxford),
[Nanopolish for Methylation](http://www.nature.com/nmeth/journal/vaop/ncurrent/full/nmeth.4184.html?WT.feed_name=subjects_computational-biology-and-bioinformatics)

2. Align the raw signal from Oxford Nanopore or PacBio reads to a reference genome to improve variant detection, detect methlyation, and/or polishing:
[Nanopolish](http://www.nature.com/nmeth/journal/v12/n8/abs/nmeth.3444.html)

3. Develop a signal-level analysis tool to detect repeat expansions/contractions from nanopore data, especially for cancer or autism genomics [NanoSatellite](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1856-3) [Dynamic Time Warping](https://en.wikipedia.org/wiki/Dynamic_time_warping)


## Genome assembly and variant calling

1. Extend GenomeScope to infer the genome characteristics of genomes with long, error-prone reads:
[GenomeScope2](https://www.nature.com/articles/s41467-020-14998-3)

2. Benchmark and/or develop a de novo assembler for polyploid genomes. Note you *should* use existing tools for overlapping, and focus on unitting/scaffolding:
[FALCON](http://www.nature.com/nmeth/journal/v13/n12/full/nmeth.4035.html)

3. Benchmark several SV callers, and create a classifier for identifying high confidence from low confidence SV calls:
[Parliament2](https://academic.oup.com/gigascience/article/9/12/giaa145/6042728)

4. Develop an enhanced SV calling algorithm that leverages known SVs:
[1000 genomes SVs](http://www.nature.com/nature/journal/v526/n7571/full/nature15394.html)
[Paragraph](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1909-7)

5. Jointly analyze (de novo assemble or index the raw reads) the genomes of multiple varieties of some species (human, rice, etc) at once to identify sequences not present in the reference genome:
[PanRice](https://academic.oup.com/nar/article/45/2/597/2333876/RPAN-rice-pan-genome-browser-for-3000-rice-genomes); [Population BWT](http://genome.cshlp.org/content/27/2/300.abstract)

6. Studying the performance of using the MinHash algorithm to bin long reads for copy number analysis or other genomics applications:
[Mash](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-016-0997-x)

7. Optimize an assembler and/or SV caller for Nanopore ultralong reads and/or PacBio HiFi reads:
[Telomere-to-telomere consortium](https://github.com/nanopore-wgs-consortium/CHM13) [HiFi reads](https://www.nature.com/articles/s41587-019-0217-9)

8. Develop methods for detecting mis-assemblies or consensus errors from long read data [Quast](http://quast.sourceforge.net/) [Clair](https://www.biorxiv.org/content/10.1101/865782v2.full)

9. Develop an Nanopore-based algorithm that leverages ReadUntil to dynammically assemble a genome with minimal coverage. [UNCALLED](https://www.biorxiv.org/content/10.1101/2020.02.03.931923v1)




## Functional Genomics

1. Benchmark different RNA-seq aligners when using a phased diploid genome compared to a standard reference genome:
[Allele-Seq](http://msb.embopress.org/content/7/1/522.long)

2. Develop an RNA-seq aligner/pipeline that incorporates variants known from the population (graph genome):
[GraphGenomes](http://biorxiv.org/content/early/2017/01/18/101378)

3. Develop methods to identify genome variants from RNAseq data, apply to individuals with many tissues profiled to identify somatic mutations:
[SNPiR](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3791257/)

4. Run ChommHMM/Segway on a phased diploid genome (NA12878) and evaluate how that compares to annotating the reference genome:
[ChromHMM](http://www.nature.com/nmeth/journal/v9/n3/full/nmeth.1906.html)

5. Run ChromHMM/Segway on a non-human species such as rice or arabidopsis:
[ChromHMM](http://www.nature.com/nmeth/journal/v9/n3/full/nmeth.1906.html), [Segway Protocol](http://biorxiv.org/content/early/2016/10/17/080382)

6. Develop ChromHMM/Segway postprocessing algorithm to label the states with their biological functions:
[Segway Protocol](http://biorxiv.org/content/early/2016/10/17/080382)

7. Explore how single cell analysis works with minimal amounts of coverage. For example, reproduce the results from the Monocle paper, and experiment with how well it performs using lower amounts of coverage:
[Monocle](http://www.nature.com/nbt/journal/v32/n4/abs/nbt.2859.html)

8. Benchmark how different single cell pipelines work at recognizing different cell types:
[MetaNeighbor](https://www.nature.com/articles/s41467-018-03282-0)


## Evolution and Disease Genomics

1. Benchmark different non-coding mutation analysis schemes on a collection of diseased genomes (cancer, autism, etc): 
[CADD](http://www.nature.com/ng/journal/v46/n3/full/ng.2892.html), [funSeq2](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-014-0480-5), [fitCons](http://www.nature.com/ng/journal/v47/n3/full/ng.3196.html)

2. Develop methods for identifying somatic mutations using high error long reads (PacBio or Oxford Nanopore)
[Short read benchmarks](http://www.nature.com/articles/ncomms10001)

3. Metagenomics: Benchmark sailfish/salmon/kallisto approaches for inferring the abundance of different species present in a population
[Meta-kalisto](https://academic.oup.com/bioinformatics/article-abstract/doi/10.1093/bioinformatics/btx106/3038398/Pseudoalignment-for-metagenomic-read-assignment?redirectedFrom=fulltext)

4. Develop a new metagenomics classifier using deep learning or other advanced ML techniques.
[PhymmBL](http://www.nature.com/nmeth/journal/v6/n9/full/nmeth.1358.html)

5. Benchmark and/or develop a method for inferring the ethnicity of an individual from their genotype:
[Genealogical DNA test](https://en.wikipedia.org/wiki/Genealogical_DNA_test)

6. Apply metagenomics approaches to identifying species present in food samples or correlated with other diseases. [AllFoodSeq](https://academic.oup.com/bioinformatics/article-lookup/doi/10.1093/bioinformatics/btw822) [Centrifuge](genome.cshlp.org/content/26/12/1721.full)

7. Investigate the rate of heterozygosity within and among human populations using consortium data. [Variation in Heterozygosity Predicts...](http://journals.plos.org/plosone/article/figure?id=10.1371/journal.pone.0063048.g001)


## CS Theory and Systems

1. Adapt one or more learned data structures for genomics data:
[Learned Data Structures](https://arxiv.org/abs/1712.01208)

2. Accelerate an important genomics pipeline using GPUs or cloud computing and use that to study a larger dataset
[Rail-RNA](https://academic.oup.com/bioinformatics/article-abstract/doi/10.1093/bioinformatics/btw575/2525684/Rail-RNA-Scalable-analysis-of-RNA-seq-splicing-and)

3. Implement a genomics processing pipeline using WebAssembly and/or Objective-C/Swift/Android [fastq.bio](https://www.smashingmagazine.com/2019/04/webassembly-speed-web-app/)

4. Develop/apply a scalable datastructure for genomics
[Sequence Bloom Trees](https://www.nature.com/articles/nbt.3442); [Mantis](https://www.cell.com/cell-systems/fulltext/S2405-4712(18)30239-4)

5. Develop a novel visualization of genomics data (especially from 23-and-me reports or single cell data):
[Circos](http://genome.cshlp.org/content/19/9/1639.full)

6. Apply deep learning techniques to a problem in genomics
[Primer](https://www.nature.com/articles/s41588-018-0295-5)

7. Develop a novel fastq/BAM compression scheme for long term storage (which may require a large precomputed dictionary and/or extensive compute)


## Or your own idea! 

This should be more than you are already doing for your PhD work, but can be a novel twist to a dataset/idea you are already using. If you have a research idea but not the right data, let me know and I'll help you find some.
