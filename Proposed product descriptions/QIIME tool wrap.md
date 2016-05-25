## QIIME Tool Wrap

### Summary
QIIME is a set of tools designed primarily for metagenomics analysis.  Wrapping a basic QIIME workflow that begins with metagenomic reads with sample information, picks OTUs in a sample, and provides several ways to visualize and compare communities would be a powerful new feature and drive the platform forward in supporting metagenomic studies.  Although we (KBase) need to be involved heavily initially to design any new data types, UI, and set the basic framework, we anticipate that QIIME developers will eventually take ownership of the tools so they can directly update versions and app-specific documentation as needed.

### Story / Description
The basic QIIME based workflow will begin with loading metagenomic reads (using existing KBase Reads datatypes), loading sample information, performing filtering or demultiplexing of the data, picking OTU counts for each sample, providing several ways to visualize/analyze the OTU counts, perform basic diversity analysis, and ideally be able to link the output into the existing KBAse community modeling tools or some of the annotation/assembly tools.  This will require possibly improved data types for handling read libraries, a data type for storing sample information, data types for OTU tables, and finally other data types to store basic analysis/processing for figures (since OTU tables will be too large to completely load on the front end).  Several new types of viewers will also be required.

### User Stories

1. A User can upload a large set of multiplexed metagenomic 16s reads (eventually shotgun as well)
2. A User can upload a metadata file to associate some minimal sample information with each read set.
3. A User can apply basic filtering and demultiplexing of the reads using QIIME
4. A User can pick OTUs from a set of reads using the built-in QIIME reference database (which we will need to map to KBase genomes) producting an OTU table (OTU count per sample) and a phylogenetic tree
5. A User can download the OTU table and phylogenetic tree
6. A User can select from among several different ways (tbd) to analyze/visualize the data and compare samples, most likely some form of diversity analysis
7. TBD - link this basic metagenomics pipeline to the other KBase tools either feeding in the community modeling tools, or perhaps options for selecting a particular OTU or set of OTUs and annotating them.


### Narrative Mockup
Not done.

### Timeline
The timeline is contingent on how we approach this Product and how much direct assistance we recieve from QIIME developers.  If we assume we will use only the existing platform and are able to get significant QIIME developer assistance, some of the functionality will be limited, but we could have a working implementation for basic components ready for QIIME developers to own in ~2 sprints.  On the other hand, we could use this Product as a driver to fix certain components of KBase.  For instance, we could use this sprint to prioritize a new Read Library data type and processing tools, drive towards a generic experimental data type, or use the OTU table as a way to do more generic things.  In this case, we can expect more on the order of 3-4 possibly non-contiguous sprints.


### Test Plan
After each sprint, we will attempt to get feedback through user testing from both 1) a biologist interested in metagenomic analysis, and 2) a QIIME developer.


### Citations
QIIME - http://qiime.org

QIIME allows analysis of high-throughput community sequencing data

J Gregory Caporaso, Justin Kuczynski, Jesse Stombaugh, Kyle Bittinger, Frederic D Bushman, Elizabeth K Costello, Noah Fierer, Antonio Gonzalez Pena, Julia K Goodrich, Jeffrey I Gordon, Gavin A Huttley, Scott T Kelley, Dan Knights, Jeremy E Koenig, Ruth E Ley, Catherine A Lozupone, Daniel McDonald, Brian D Muegge, Meg Pirrung, Jens Reeder, Joel R Sevinsky, Peter J Turnbaugh, William A Walters, Jeremy Widmann, Tanya Yatsunenko, Jesse Zaneveld and Rob Knight; Nature Methods, 2010; doi:10.1038/nmeth.f.303
