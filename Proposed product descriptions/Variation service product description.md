# Variation Service Product Description

### Summary

The variation service will enable users to compare closely related
genomes and identify SNPs, MNPs, insertions and deletions. These
variations will be catalogued along with annotations (gene vs
intergenic, synonymous vs nonsynonymous, frameshift, protein function,
neighboring features, etc). When multiple genomes are selected to be
compared with a reference genome, a summary table showing the shared
variations will also be presented. This service will allow users to
zoom in on a few critical variations that might be the determinants of
their phenotypic differences.

### Story/Description
TODO

### User stories
- User A has 9 closely related strains that exhibit two different
  phenotypes. She uses the variation service to find out there are 7
  variations among them including 6 synonymous SNPs, 1 large
  intergenic indel, 1 frameshift, and 1 nonsynonymous SNP. She decides
  that the latter three variations may be the cause of the phenotypic
  difference and tries to verify their effect with experiments.
- User B has a set of 50 strains that have all evolved from the same
  genomes for several generations. He wants to understand why some of
  these strains have acquired a new phenotype while don't. Because
  these strains have accumulated many mutations from the original
  genome, he asks the variation service to derive a consensus
  reference sequence for them. He then views the variations in terms
  of this new reference sequence and find a small list of MNPs that
  might be the reason behind the new phenotype. He proceeds to confirm
  this hypothesis with experimental approaches. 

### Narrative Mockup
TODO

### Timeline
TODO

### Test plan
TODO

### Citations
- BWA-MEM
- Bowtie2
- Last
- FreeBayes
- Samtools
