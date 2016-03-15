## RNA-seq pipeline v2

### Summary
Update the RNA-seq pipeline in KBase to make it more modular and scalable (requires additional platform support - details below). Also offer additional tools that reduce compute and improve usability.

### Story/Description
List of updates to the existing pipeline:
1. Enable/modularize the Tuxedo pipeline based on standalone methods.
2. Update the Tuxedo pipeline to use new version of Genome.
3. Add quality check tools for RNA-seq reads such as FastQC and enable existing ones such as Trimmomatic.
4. Build downloaders for RNA-seq datatypes.
5. Additional visualization support for output alignments, etc

Review and prototype additional tools that reduce compute and improve usability.
1. STAR / Rockhopper
2. EdgePro / StringTie
3. DESeq
4. Kallisto-Sleuth


### Platform dependency:
1. Bulk Uploaders
2. Ability to scale a compute-intensive job using multiple AWE workers or HPC


### Timeline
3-4 sprints

### Test plan
1. Test scalability for 50-100 samples for bulk upload
2. Test scalability for 50-100 samples for all compute-intensive methods, incl. alignment

### Citations
1. STAR: http://bioinformatics.oxfordjournals.org/content/early/2012/10/25/bioinformatics.bts635
2. EdgePro: http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3603529/
3. StringTie: http://www.nature.com/nbt/journal/v33/n3/full/nbt.3122.html
4. DESeq: http://genomebiology.biomedcentral.com/articles/10.1186/gb-2010-11-10-r106
5. Kallisto: https://pachterlab.github.io/kallisto/about.html



