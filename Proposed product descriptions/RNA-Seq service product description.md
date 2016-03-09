#RNA-Seq Service Product Description

##Summary
The present version of RNA-Seq service (RNA-Seq v1.0) is essentially an implementation of the RNA-Seq Tuxedo protocol for prokaryotes and eukaryotes. Currently, it provides an integrated computational workflow for RNA-Seq based gene expression analysis for microbes and flagship plant genomes. This service aligns the RNA-Seq reads, assigns aligned reads to genes and performs differential gene expression analysis to detect differential transcript abundances between tissues, developmental stages, genetic backgrounds, and environmental conditions.

Ultimately this service will support a wide range of transcriptome data analysis needs such as gene discovery and annotation, gene fusion detection, allele-specific expression, and de novo transcriptome assembly.

##Extended Description
RNA-Seq pipeline allows the user to upload raw sequence reads from an experiment that involves two or more conditions. Next the reads are mapped to a reference genome using Bowtie2 for microbes and TopHat for plant genomes. The read alignments per sample are provided as input to Cufflinks, which assembles the alignments to  transcripts. TopHat and Cufflinks are run on each individual sample and biological replicates independently. Then, the independently assembled transcripts from each sample are merged using Cuffmerge to a unified transcriptome for further analysis. Cuffdiff uses the merged transcriptome and the read alignments from each sample to identify the differentially expressed genes. The outputs from all the above mentioned methods are saved as workspace objects. The Cuffdiff files are visualized using CummeRbund package to facilitate exploration of genes such as density plots, scatter plots, volcano plot, PCA plots, MDS plots etc. 

In nutshell, we would like to have applications and methods that will allow users to run RNA-seq pipeline using Tuxedo protocol (Cufflinks,Cuffmerge,Cuffdiff, CummeRbund) that follows these steps:

1. Upload the sequence reads file into the Narrative
2. Conduct sequence quality check
3. Collect metadata for the experiment
4. Map reads using Bowtie2 or TopHat
5. Assemble transcripts with Cufflinks
6. Merge transcripts using Cuffmerge
7. Identify differential expression using Cuffdiff
8. Create the expression matrix
9. Visualize the output 
+ Alignment statistics using Pie Chart, 
+ Sample Gene expression in a histogram, 
+ Visualization of different plots using CummeRbund plots such as density plots, scatter plots, Volcano plot, PCA plots, MDS plots etc. 

Note: RNA-seq pipeline using the Tuxedo protocol requires the reference genome annotation in GTF format and the reference genome in FASTA format. Currently in the pipeline, we get the FASTA formatted reference genomes using the ContigSet objects and the reference annotations being manually uploaded by a KBase developer. We expect that, once we have the new genome model in production, the method to create the reference genome annotation and getting genome in FASTA will be supported by a either a Data API call to the genome object or a new method to the object types required. *This is conditional to the availability of Genome object in production by Feb 1, 2016.*

Citation: Trapnell C, Roberts A, Goff L, Pertea G, Kim D, Kelley DR, Pimentel H, Salzberg SL, Rinn JL, Pachter, L (2012) Differential gene and transcript expression analysis of RNA-seq experiments with TopHat and Cufflinks. Nature Protocols, 7(3), 562 578. http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3334321/


##Timeline for feature release
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



##User Stories

1. E. coli User story:

For this narrative, the published study was used to characterize the transcriptome of wild type E. coli K-12 MG1655 genome under low and high Mg+2 concentration to examine the changes in the gene expression to explore KBase apps and methods related to expression data analysis.
The raw reads were generated from the wild type E. coli cultures during exponential phase in N-minimal media supplemented with 10mM MgCl2(high Mg+2 conc.) and 10 uM MgCl2 (lower Mg+2 conc.),  which causes repressing and inducing conditions for the PhoQ/PhoP two-component system respectively. 

Mockup Narrative: RNA-Seq pipeline testing using E. coli sRNA studies to identify Mg+2 dependent sRNAs
https://narrative-ci.kbase.us/narrative/ws.3387.obj.1

2. Arabidopsis User story:
Light is one of the most important stimuli to plant development. In Arabidopsis, the seedling hypocotyl has emerged as an exemplar model to study light control of cell expansion. Seedlings grown in the light show a short hypocotyl with green and expanded cotyledons, whereas dark grown seedlings show a long hypocotyl with yellow and unopened cotyledons. LONG HYPOCOTYL 5 (HY5) is a basic leucine zipper transcription factor that functions downstream of multiple families of photoreceptors. Mutations in the HY5 gene cause many diverse abnormal phenotypes in Arabidopsis, including elongated hypocotyl, reduced accumulation of pigments, halted chloroplast development in greening hypocotyls, altered root morphology, and defective hormonal and stimulus responses. HY5 thus plays a central role in the coordination of light signaling and appropriate gene expression suggesting that HY5 could act as a signal transducer that links various signaling pathways to coordinate development. 

For this narrative, the published study on RNA sequencing to examine HY5 mediated gene expression changes between wild-type and hy5 mutant plants was used to explore KBase apps and methods related to expression data analysis.

Mockup Narrative: Arabidopsis Transcriptome Analysis based on Wild and Mutant Studies using RNA-Seq Pipeline
https://narrative-ci.kbase.us/narrative/ws.3548.obj.1
