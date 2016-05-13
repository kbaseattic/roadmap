## Microbial Variation Service Product Description

### Summary

The variation service will enable users to compare closely related
genomes and identify SNPs, MNPs, insertions and deletions. These
variations will be catalogued along with annotations (gene vs
intergenic, synonymous vs nonsynonymous, frameshift, protein function,
neighboring features, etc). When multiple genomes are selected to be
compared with a reference genome, a summary table showing the shared
and unique variations will also be presented. This service will allow
users to zoom in on a few critical variations that might be the
determinants of the phenotypic differences and hence targets for
experimental validation.

+ Team lead: Fangfang Xia

+ Team: Rida Assaf, Chris Bun, John Santerre

### Description

The variation service is designed to be part of the comparative
genomics services. It will help users identify local DNA variations
including SNPs, MNPs, indels, and small intergenic variations. This
level of comparative analysis is particularly applicable to sets of
closely related genomes that exhibit different phenotypes. The result
of the variation analysis could illustrate the evolutionary trajectory
of the genetic basis for new phenotypes. The genetic variants
identified in this service also form the input for downstream analyses
such as comparative metabolic modeling or whole genome association
study (GWAS).

A typical variation analysis workflow consists of the following main steps:

1. Map short reads of each sample to the reference genome
2. Call variations on the individual and merged read alignments
3. Annotate the position and effect of the identified variations
4. Summarize the variations and highlight the common or high-confidence ones

There are multiple tools that can be used for most of these steps. And
the variation analysis of eukaryote genomes can be more complicated
and involve more tools. We propose to initially support the following tools:

+ Read mapping: BWA-MEM, Bowtie2, MOSAIK (optional), LAST (optional)
+ Variation calling: FreeBayes, Samtools
+ SNP annotation: SnpEff


### User Stories
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
  
- User C uses the varation service to identify a intergenic mutation
  among her two groups of very closely related genomes. Upon further
  investigation, she believes the region where this mutation took
  place and appeared to have altered the phenotype of the strain is
  actually a short protein that was missed by the original gene caller.
  
- User D suspects his genetically engineered strains have accumulated
  mutations in his lab. He identifies 3 shared frameshifts and many
  SNPs in a group of these strains that have a different phenotype. He
  constructs a metabolic model for this strain and plays out the
  consequence of the frameshifts through comparative modeling. He also
  feeds the SNPs into microbial GWAS to identify combinations of SNPs
  that are trait specific.
  

### Narrative Mockup

Variation location and type
![Image of variation location](https://raw.githubusercontent.com/kbase/comparative_genomics/master/docs/images/var-types.png)

Variation region and functions of neighboring proteins
![Image of variation function](https://raw.githubusercontent.com/kbase/comparative_genomics/master/docs/images/var-functions.png)

Table summarizing shared and unique variations across samples
![Image of variation samples](https://raw.githubusercontent.com/kbase/comparative_genomics/master/docs/images/var-samples.png)


### Timeline
+ Sprint 1: define variation data types; implement a prototype backend workflow with BWA-MEM and FreeBayes
+ Sprint 2: add support for additional tools (Bowtie2, FreeBayes, and optionally MOSAIK and LAST)
+ Sprint 3: summarize the variants across samples; implement output widget; add download support for VCF files
+ Sprint 4: implement the ability to infer reference sequence via consensus; testing; documentation;

### Test Plan

We will test the sequence comparison methods internally with sets of
genomes of varying distances. We will also attempt to get feedback
through user testing from biologists and bioinformaticians on their
own datasets.


### Citations
- BWA-MEM
- Bowtie2
- LAST
- MASAIK
- FreeBayes
- Samtools
- SnpEff
