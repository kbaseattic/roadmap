## Support for phytozome as source of genomes in KBase 
### Summary
The source of plant genomes in KBase is either Refseq or Ensembl plants. Many plant genomes sequenced by JGI are only available through phytozome (https://phytozome.jgi.doe.gov/pz/portal.html). We need to add these genomes to KBase as KBaseGenomeAnnotations.GenomeAnnotation typed object. 
### Story/Description
We have limited number of plant genomes in KBase. We prioritized RefSeq and Ensembl plants as data sources because they had genomes in Genbank format. The genomes available through phytozome are only available in gff/fasta/extras format and so they were not supported in the first round. Most of the missing genomes are of great interest to DOE funded researchers and we should support them sooner than later. More generally, we need to support gff/fasta/extras format as input for adding genomes to KBase.
### User stories
Addition of each new plant genome will support a new community of researchers working on that genome. These researchers can use KBase apps like RNA-seq and FBA modeling and cite KBase if they find it useful.
Most eukaryotic genome annotation tools output genome data in gff/fasta/extras (and not Genbank format). So support for gff/fasta/extras format will open up KBase for researchers who have done their sequencing outside of JGI and want to keep the genome private before publication.
 

### Timeline

One sprint

### Test plan
Internal testing will include use of data_api to fetch genome annotation data, as well as using the landing pages to navigate the annotation information. We will also need to make sure they work as expected with RNA-seq workflow and FBA modeling tools.

Same plan for external users who will work on this with their own dataset.
### Citations
Phytozome is a DOE funded project.
