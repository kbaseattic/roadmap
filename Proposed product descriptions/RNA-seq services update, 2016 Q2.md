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

### Risks and dependencies
1. It is **essential** that we have a clear path to uploaders. However, it's presently not very apparent what that path is. Here are a few high priority uploader feature requests.
  1. Import from http/ftp URL in Narrative Interface
  2. Support multiple job uploads in Importer to allow parallel uploads in a single narrative session.
  3. SRA Format (eg NCBI genomes): SRA->FASTQ support in uploader. 
2. Bulk Uploaders are on the plate for Q2
  1. Make sure to capture metadata about the samples at upload
3. Ability to scale a compute-intensive job using multiple AWE workers or HPC is currently absent in KBase and it would be desirable to have that be supported in very near future, since it will allow us to batch process functionality such as TopHat, Cufflinks or run entire Tuxedo pipeline end-to-end after setting the parameters in a single app.
4. A genome browser, such as JBrowse, is desirable for viewing BAM alignments




