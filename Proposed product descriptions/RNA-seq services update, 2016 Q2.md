## RNA-seq service update, 2016 Q2

### Summary
In this campaign, we will update the RNA-seq service to include support for the new Genome data object via the Data API, new downloaders, additional interactive widgets and plots. As a result, this will also include refactoring of the current functionality and related modifications in apps and documentation.

### User Stories
1. User can upload a new genome that does not exist in KBase. He would be able to upload the annotations and assembled sequences in and can use that genome as a reference Genome in the RNA-seq service
2. User can run RNA-seq pipeline on the reference genomes stored in KBase. The reference genomes can be from Refseq, Ensembl and Phytozome. 
3. User can run TopHat on the read files that he has uploaded and visualize output alignments in Narrative UI and download the alignments.
4. User can download the Cufflinks and Cuffdiff output files.
5. User can select the subset of samples to visualize interactively the Cuffdiff results obtained from the entire set of read samples using CummeRbund package, and can get HeatMap of the selected samples. Then user can  download the plots and HeatMap as high resolution static images.  
6. User can run interactive method “Volcano Matrix Plot” to get the list of significant differentially expressed genes and can also download the static plots and the associated list of genes.
7. User can see the functional information and GO annotations on the list of differentially expressed genes in Expression matrix and HeatMap.
8. User can upload multiple read files in a single upload (bulk uploader dependency).
9. User can upload read files from ftp/http site using the data importer.

### Test plan
1. Integration tests based on new version of Data API as well as uploaders, downloaders, landing pages, widgets.
2. Conduct external beta tests

### Existing bottlenecks, Dependencies and Resolutions
#### Uploader for reads to include SRA format (addresses read upload performance in Q2):
In addition to FASTQ format, we would like to have reads uploader in SRA format. It will help in faster upload and will be convenient for users to directly import the file from ftp site in SRA format in narrative. Just to give an idea - read file SRR676520 in SRA format is 2.4Gb. Currently, we need to convert it in FASTQ format to upload it in narrative. Once we convert it in FASTQ through SRA toolkit, its size becomes 17.8 Gb. Here are the steps a user has to currently do to import reads -
1. Install NCBI SRA toolkit on the desktop
2. Download read files (individually for each sample in SRA format) from NCBI SRA site
3. Convert SRA to FASTQ on the desktop
4. Upload file from desktop to narrative using “import”
 
So, it’s very tedious process that takes lot of memory and time in uploading FASTQ file. SRA format is almost 7-8 times smaller in size so it will also fasten the uploading process and user can directly upload file from NCBI FTP site without going through all the steps on his desktop.
 
As RNA-seq tool requires reads in FASTQ format, therefore, it’s important to convert imported reads from SRA to FASTQ format. This will be supported by the Bulk upload team in this quarter. https://atlassian.kbase.us/browse/KBASE-4106
 
#### Bulk Uploader and Metadata (address usability w.r.t uploading large number of samples and modularity in pipeline in Q2)
During discussion with Bulk upload and Data teams, we discussed the RNA-seq dependency on bulk uploader and metadata.
We will prioritize some of the metadata that needs to filled by user at the time of bulk uploading of the reads. Some of the metadata can be asked later by narrative method. As a result, the ‘Set up RNA-seq Experiment’ method that creates experiment analysis object as first step will no longer be the requirement of the pipeline. Rather, metadata information as part of RNA-seq analysis project report will be input parameters as part of cuffdiff method.
 
Also, with help from Bulk upload team, we are considering supporting bulk upload for BAM files in RNA-seq service in next quarter.

Metadata list is given here on this link:
https://docs.google.com/document/d/17Dfp_3Qjrb-TDedGaDnT9EL7cnKXiXCrbxBVN2kvgwc/edit

#### Modularity (addresses usability and scalability to some degree in Q2)
We would like to have modular TopHat and Cufflinks methods. In addition, Cuffmerge and Cuffdiff can be merged as one method.

We have agreed on making some datatype changes for the RNA-seq module.
1. The user uploads the reads using the bulk uploader, which will create the corresponding (Single/Paired)EndLibrary objects. In future, RNA-seq specific bulk uploader will create RNASeqSample(s).
2. Earlier, ‘Set up RNA-seq Analysis’ method was needed to keep track of the updates in the pipeline using the Analysis object. This method has been updated. Instead, the user will simply create a RNA-seq sample set using Method #3.
3. Method #3: User provides the read library objects. It will create RNASeqSampleSet and user-hidden GFFAnnotation. In future, it will be replaced by the GFF file retrieved from the GenomeAnnotation using the Blob API. RNASeqSampleSet will have all the metadata associated with the read files.
4. Methods #4, #5, #6: Earlier, the user had to invoke #3 and #4 methods once per each sample. Now, the user runs them once per one sampleset. The user provides only RNASeqSampleSet and tools options. Corresponding output objects will be generated by default using sample read file labels. User does not need to provide individual sample inputs or corresponding sample outputs. 
5. RNASeqSampleAlignment, RNASeqSampleExpression, RNASeqDifferentialExpression objects are meant to be generic enough and will require minimal or no refactoring when the Euks team brings next generation of RNA-seq tools in the coming quarter.

Currently we have derived objects from KBaseGenomes.GenomeAssembly and KBaseGenomes.GenomeAnnotation for Bowtie Index file and GTF file (as Genome Reference Annotation) respectively. These are fundamentally not biological data types and can be stored as binary files associated with a primary datatype, e.g. Bowtie index with Assembly and GTF with Genome Annotation. We have agreed to work with Data team to make the necessary changes in next quarter.

#### Scalability (not addressed in Q2)
Please note that, this PD is primarily addressing the modularity, usability and to some extent scalability issues, we will continue to have scalability concerns for large number of samples and large reads and large genomes, common to Euks.

TopHat and Cufflinks can be scaled up by Parallel SDK job execution support and Cuffmerge/Cuffdiff can be scaled up by HPC based execution support in near future when the corresponding PDs are implemented in KBase.




