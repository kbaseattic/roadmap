# RNA-seq Service Product Description

## Summary
The present version of RNA-seq service (RNA-seq v1.0) is essentially an implementation of the RNA-seq Tuxedo protocol for prokaryotes and eukaryotes. Currently, it provides an integrated computational workflow for RNA-seq based gene expression analysis for microbes and flagship plant genomes. This service aligns the RNA-seq reads, assigns aligned reads to genes and performs differential gene expression analysis to detect differential transcript abundances between tissues, developmental stages, genetic backgrounds, and environmental conditions.

Ultimately this service will support a wide range of transcriptome data analysis needs such as gene discovery and annotation, gene fusion detection, allele-specific expression, and de novo transcriptome assembly.

## Extended Description
RNA-seq pipeline allows the user to upload raw sequence reads from an experiment that involves two or more conditions. Next the reads are mapped to a reference genome using Bowtie2 for microbes and TopHat for plant genomes. The read alignments per sample are provided as input to Cufflinks, which assembles the alignments to  transcripts. TopHat and Cufflinks are run on each individual sample and biological replicates independently. Then, the independently assembled transcripts from each sample are merged using Cuffmerge to a unified transcriptome for further analysis. Cuffdiff uses the merged transcriptome and the read alignments from each sample to identify the differentially expressed genes. The outputs from all the above mentioned methods are saved as workspace objects. The Cuffdiff files are visualized using CummeRbund package to facilitate exploration of genes such as density plots, scatter plots, volcano plot, PCA plots, MDS plots etc. 

In nutshell, we would like to have applications and methods that will allow users to run RNA-seq pipeline using Tuxedo protocol (Cufflinks, Cuffmerge, Cuffdiff, CummeRbund) that follows these steps:

1. Upload the sequence reads file into the Narrative
2. Collect metadata for the experiment
3. Map reads using Bowtie2 or TopHat
4. Assemble transcripts with Cufflinks
5. Merge transcripts using Cuffmerge
6. Identify differential expression using Cuffdiff
7. Create the expression matrix
8. Visualize the output 
9. Sample Gene expression in a histogram 
10. Visualization of different plots using CummeRbund plots such as density plots, scatter plots, Volcano plot, PCA plots, MDS plots etc. 

Note: RNA-seq pipeline using the Tuxedo protocol requires the reference genome annotation in GTF format and the reference genome in FASTA format. Currently in the pipeline, we get the FASTA formatted reference genomes using the ContigSet objects and the reference annotations being manually uploaded by a KBase developer. We expect that, once we have the new genome model in production, the method to create the reference genome annotation and getting genome in FASTA will be supported by a either a Data API call to the genome object or a new method to the object types required. *This is conditional to the availability of Genome object in production by Feb 1, 2016.*


## Timeline for feature release
+ Merge ‘Setup RNA-Seq Analysis’  and ‘Associate Reads to RNASeqSample’ methods - Jan 31 , 2016
+ Merge ‘Align Reads to Tophat’ and ‘View Alignment Statistics’ methods - Jan 31, 2016
+ Merge ‘Assemble Transcripts using Cufflinks’ and ‘View Expression Histogram’ methods - Jan 31, 2016
+ Improve the method ‘View Alignment Statistics’ - Jan 31, 2016
+ Add Report type widgets to the RNA-Seq methods - Feb 5, 2016
+ Coordinate with the Data team for getting the genome annotation in GTF formats.
+ Testing the use cases for the RNA-Seq methods in CI - Jan 29, 2016
+ Deploying the KBaseRNASeq service in Next - Jan 31, 2016
+ Testing the use cases for the RNA-Seq methods in Next - Jan 31, 2016
+ RNA-Seq service needs few minors updates after the Genome object is available in Production. 
+ Deploying the KBaseRNASeq service in Production  - Feb 12, 2016. *This is conditional to the availability of Genome object in production by Feb 1, 2016.*
+ Testing the use cases for the RNA-Seq methods in Production -  Feb 19, 2016. *This is conditional to the availability of Genome object in production by Feb 1, 2016.*
+ Creating the narratives for RNA-Seq using KBase RNA-Seq pipeline - Feb 26, 2016


## User Stories
1. [Arabidopsis: Wild vs. Mutant Studies (single-end reads)](https://narrative.kbase.us/narrative/ws.13382.obj.1)
2. [E Coli: Wild vs. Mutant Studies (single-end reads)](https://narrative.kbase.us/narrative/ws.13442.obj.3)
3. [Pseudomonas: Wild vs. Mutant Studies (paired-end reads)](https://narrative.kbase.us/narrative/ws.13397.obj.2)


## Citation: 
[Trapnell C, Roberts A, Goff L, Pertea G, Kim D, Kelley DR, Pimentel H, Salzberg SL, Rinn JL, Pachter, L (2012) Differential gene and transcript expression analysis of RNA-seq experiments with TopHat and Cufflinks. Nature Protocols, 7(3), 562 578.](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3334321/)
