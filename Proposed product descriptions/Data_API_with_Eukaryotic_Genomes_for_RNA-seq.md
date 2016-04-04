# Data API with Eukaryotic Genomes for RNA-seq

## Summary

This campaign will improve the KBase user experience and resolve standing issues with Data. The campaign has two main objectives: (1) integrate the new Genome types with the system, so that users can upload Eukaryotic data; this will help us better understand the issues involved when updating existing types in the system, and (2) enable RNA-seq on Eukaryotic data uploaded by users.

## User Stories

As a KBase user with Eukaryotic annotations and assembled sequences in Genbank format, I need a way to upload my Assembled Sequences and Annotations in full so that I can use that as a reference Genome for RNA-seq analyses.

As a KBase user with Eukaryotic annotations in GFF format and Assembled sequences in FASTA format, I need a way to upload my data and use it as a reference Genome for RNA-seq analyses.

As a KBase user that has uploaded some large Eukaryotic Assembly and Annotation data, I need to perform an RNA-seq analysis on my data, view the Expression results, and be able to connect to other KBase apps/methods from there.

As a KBase user that has uploaded some large Eukaryotic Assembly and Annotation data, I need a way to view my data in the Narrative UI and from Data Landing Pages.

As a KBase user that has used the RNA-seq apps/methods, I would like to be able to download the alignments produced.

As a KBase user that has used the RNA-seq apps/methods, I would like to be able to download the static analysis plots produced.

As a KBase user that has used the RNA-seq apps/methods, I would like to be able to download the output files produced by Cuffdiff.

As a developer of the RNA-seq pipeline, I need a simple way to get back specific file formats of data using the Data API.

## Timeline

### Estimated staging

### Data API support for refactoring RNA-seq

* Add Data API methods for retrieving specific file format representations of data (GFF, FASTA, GTF)
* Address pain points identified by RNA-seq team in refactoring code to use Data API

### Enable User Plant data uploads

* Integrate new Genome type uploaders with Narrative UI
* Implement GFF upload process for GenomeAnnotation
* Upload testing with real data from multiple sources

### RNA-seq results for new Genome types

* Update output of RNA-seq (ExpressionMatrix type) and any code that touches ExpressionMatrix to be compatible with new Genome types

### Type compatibility until full system support for Data API

* Converter (lossy) from new Genome types (GenomeAnnotation, Assembly, Taxon) to old types (Genome, ContigSet) for system compatibility

### Enable User Plant data and RNA-seq downloads

* Implement new Genome type downloaders
* Implement RNA-seq data downloaders for output from TopHat, Cuffdiff, Cummerbund

### Additional improvements (Stretch goals)

* Improve Reads data types and uploaders
* Improve Data Landing Pages for Genome types
* Add or Improve Data Landing Pages for RNA-seq Data types
* Sharing corrections for RNA-seq related Data Types (ContigSet, ExpressionSample)
* Data API sharing mechanism to fix handles not being shared publicly
* Coordinate with UI on public Narrative sharing issues
    
## Test Plan

* Data API code uses TravisCI for unit tests
* Integration tests with RNA-seq can be performed manually from the Narrative UI

## Risks

* Possible system changes to upload or download during Q2 could significantly delay any work connected to uploaders or downloaders, which are a key set of items in this campaign.
* Reference data updates from Phytozome would also rely on dealing with GFF data, creating a dependency on this campaign.  Moving that work up in this campaign would cause problems in determining early API work that could take longer than expected.
* Incomplete or unstable conversion of RNA-seq methods to use the Data APIs (described in a parallel campaign) could lead to newly uploaded Eukaryotic genomes not being usable as RNA-seq inputs.
* Known performance issues with the current data stores for large data objects could be exacerbated by the additional load from the RNA-seq pipeline, requiring some performance-focused refactoring of object representations to file based storage.

## Citations


