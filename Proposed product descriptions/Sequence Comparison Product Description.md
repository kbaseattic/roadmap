#Sequence Comparison Product Description

##Summary

The sequence comparison service will enable users to compare closely
related genomes on the DNA sequence level in the form of two narrative
methods: (1) DNA sequence comparison, and (2) whole genome alignment.

The DNA sequence comparison method will take two or more assembled
genomes and compute the number of single-base differences (mutations
and indels) in any genome pair using DNAdiff. The resulting all-to-all
similarities will be presented in a matrix along with textual reports.

The whole genome alignment method will take two assembled genomes and
align them using Mugsy or Mauve. These methods will align stretches of
very long nucleotides in millions of bases and detect the presence of
rearrangements, duplications, and large-scale sequence gain and
loss. The output will include a circular whole genome rearrangement
graph and downloadable alignment files.

These two methods will be part of a future comparative genomics app
which will also tie in improved proteome comparison, pangenome
analysis and a new variation service. The goal of this app is to
integrate all levels of genomic differences identified using various
comparative methods and connect them to phenotypic differences.

+ Team lead: Fangfang

+ Team: Rida Assaf, Harry (UI)

##Extended description

The proposed sequence comparison methods are designed to be part of
the comparative genomics service that will enable users to compare
multiple genomes on multiple levels.

1. Protein family (presence/absence, homology, copy number variations)
2. Protein sequence similarity
3. DNA sequence similarity (fraction identity, coverage)
4. Genome rearrangements
5. DNA local variations (SNPs, MNPs, indels, intergenic variations)

The existing narrative methods (pangenome analysis and proteome
comparison) partially address 1 and 2. We are filling in 3 and 4 with
the two proposed methods here. 5 will be addressed by a variation
service with SNP annotation in the future. Coupled with a phylogenetic
framework, these five levels of comparisons will form the basis of a
comparative genomics app that will allow users to identify a whole
spectrum of genetic differences, analyze them in an evolutionary
context, and connect them to phenotypic differences with metabolic
models, statistical methods (GWAS) and machine learning frameworks. 

Compared to protein level comparative methods, the two sequence
comparison methods proposed here are particularly applicable for
closely related genomes such as:

+ two strains of the same species
+ two assemblies of the same organism
+ a draft assembly and a closely related finished genome

We will be wrapping third-party tools DNAdiff, Mugsy and Mauve for
backend computation in this phase. A tool that visualizes the whole
genome rearrangement in a circular fashion (see the mock narrative
output below) will also wrapped. More whole genome alignment methods
(over 10 competed in Alignathon) will be considered in the future.

For sequence comparison, DNAdiff identifies SNPs and single base
indels. These will only be presented in a textual output in this phase
as no analysis can currently consume SNPs. More robust SNP
identification will be part of the future variation analysis which
will be able to take raw reads as input.

For whole genome alignment methods, a common output format is MAF
(multiple alignment format). However, there are few tools and none in
the current KBase narrative that can process MAF files. So we will
convert the output to the FASTA alignment format. They could be used
for tree building. 

##Timeline for feature release
+ January 15: deploy a prototype of the DNA sequence comparison method into narrative-ci
+ January 29: deploy a prototype of the whole genome alignment method into narrative-ci
+ February 5: improve narrative UI for both methods (visual output and downloadable files)
+ February 19: deploy both methods to production

##User stories
+ User Esther sequences and assembles what she thinks is the same
  genome twice with slightly different sequencing platforms. She would
  like to know if mutations have occurred in the 18-month period
  between the two samples. She uses the DNA sequence comparison method
  and the whole genome alignment method to identify the exact
  differences (SNPs and rearrangement) between the two sets of
  assembled contigs.

+ User Tina has six strains that exhibit two groups of markedly
  different phenotypes. She runs the proteome comparison and finds no
  protein-level difference among the strains. She wonders if the
  phenotypic difference could be a result of a few SNPs or genome
  arrangements. She uses the DNA sequence comparison and whole genome
  alignment methods to identify a total of 5 SNPs and 2kb long
  translocation that separates these two phenotypes.


##Narrative mockup

The input widget of these two methods will allow a user to select two
or more genomes a la the proteome comparison and the pangenome
methods. The output for each method is presented in mock graphics
below.

### DNA sequence comparison

![Image of DNAdiff similarity matrix](https://raw.githubusercontent.com/kbase/comparative_genomics/master/docs/images/DNAdiff-matrix.png)

![Image of DNAdiff report](https://raw.githubusercontent.com/kbase/comparative_genomics/master/docs/images/DNAdiff-report.png)

### Whole genome alignment

![Image of Genome Rearrangement](https://raw.githubusercontent.com/kbase/comparative_genomics/master/docs/images/Genome-rearrangements.png)

## Test Plan

We will test the sequence comparison methods internally with sets of
genomes of varying distances. We will also attempt to get feedback
through user testing from biologists and bioinformaticians on their
own datasets.

##Citations to code sources
+ DNAdiff
+ Mummer
+ Mugsy
