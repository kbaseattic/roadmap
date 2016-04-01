## RNA-seq service update

### Summary
In this campaign, we will update the RNA-seq service to include support for the new Genome data object via the Data API, new downloaders, additional interactive widgets and plots. As a result, this will also include refactoring of the current functionality and related modifications in apps and documentation.

### Story/Description
1. Enable/modularize the Tuxedo pipeline based on standalone methods.
  1. Create new method that runs TopHat immediately on a single sample
  2. Create a method to run CuffMerge and CuffDiff in a single step
  3. Note there are logical dependencies that make it impossible to run certain components out of sequence. It is not possible to run Cufflinks or later tools without first aligning the reads using Bowtie/Tophat/others. Also note that cufflinks is already generic in the sense that either Bowtie or TopHat can be used for aligning the reads.
2. Update the Tuxedo pipeline to use new version of Genome.
3. Provide UI elements to control mandatory and advanced/optional parameters
  1. Review mandatory and advanced options to make sure all the important ones are exposed and system parameters are autoset
4. Extend current functionality to get annotations for new genome objects. Also, precompute and load annotations for reference genomes
5. Precompute Bowtie indexes for all reference genomes in data store
6. Add downloaders for RNA-seq datatypes (reads, alignment, cuffdiff output, cummerbund plots).
7. Additional visualization support for output alignments, including [iobio](http://bam.iobio.io/). 

### Test plan
1. Integration tests based on new version of Data API as well as uploaders, downloaders, landing pages, widgets.
2. Conduct external beta tests

### Risks and dependencies
1. It is *essential* that we have a clear path to uploaders. However, it's not presently very apparent what that path is.
  1. Import from http/ftp URL in Narrative Interface
  2. Support multiple job uploads in Importer to allow parallel uploads in a single narrative session.
  3. SRA Format (eg NCBI genomes): SRA->FASTQ support in uploader. 
2. Bulk Uploaders are on the plate for Q2
  1. Make sure to capture metadata about the samples at upload
3. Ability to scale a compute-intensive job using multiple AWE workers or HPC is currently absent in KBase and it would be desirable to have that be supported in very near future, since it will allow us to batch process functionality such as TopHat, Cufflinks or run entire Tuxedo pipeline end-to-end after setting the parameters in a single app.
4. A genome browser, such as JBrowse, is desirable for viewing BAM alignments




