## Transfer The JGI Plant Gene Atlas Data to KBase

### Summary
The JGI Plant Gene Atlas project produces a standardized expression atlas across diverse tissues, broad range of treatments/conditions, and time series from JGI plant flagship genomes and model plant genomes. Phytozome has acquired this collection of RNA-seq expression data from several collaborative projects internally and externally.

The JGI Plant Gene Atlas data will be available through Phytozome and we need to add this Gene Atlas data to KBase from JGI Gene Atlas Portal.

### Story/Description
Currently, we have limited number of plant expression data available in KBase. We would like to leverage the JGI Plant Gene Atlas data in the KBase Narrative for RNA-seq workflow and downstream analysis either in metabolic models or co-expression network analysis. There can be two ways that the JGI Gene Atlas data can be added to KBase.
1. The quality single-end or paired-end reads from the JGI Gene Atlas data can be loaded in FASTQ format from the JGI Gene Atlas Portal and added as “KBaseAssembly.SingleEndLibrary” or KBaseAssembly.PairedEndLibrary typed objects to the dedicated workspace.

2. The raw transcriptome data obtained from Cufflinks can also be transferred to KBase and added as KBaseRNASeq.RNASeqCuffmergetranscriptome typed object to the dedicated workspace.
 
The published reads and the transcriptome data can be made available to the KBase users via the “Public” tab and thus, this data can be imported as individual files in narratives. The read files can be used to run Tuxedo RNA-seq workflow whereas raw transcriptome data can be used to run cuffdiff plots and to create expression matrix. The expression matrix can be used further in downstream analysis either in metabolic models or co-expression network analysis.
 
### User stories
1. The JGI Plant Atlas Data will support a new community of researchers especially JGI researchers who are working on the flagship genomes. These researchers will be able to use the several KBase narrative methods associated with RNA-seq pipeline, Feature-value Pipeline (multiple clustering algorithms) and FBA modeling tools and KBase will be a great platform for these users for downstream analysis. This way KBase will also be cited in their publications.
 
2. Other researchers can easily get access to the “published” JGI Plant Atlas Data in their narrative using “Public” tab. This way, a new community of researchers will also be able to leverage the standardized collection of high-throughput sequence data obtained from JGI in their own narratives.
 
 
### Timeline
Do not know yet. Need to contact JGI Gene Atlas group to get more information on the availability of the Data Set on Phytozome Gene Atlas Portal.
 
### Test plan
We need to make sure the imported Gene Atlas data must work as expected with RNA-seq workflow and FBA modeling tools.

