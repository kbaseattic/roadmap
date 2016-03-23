## Wrapping Assemblers with SDK Product Description

### Summary

This effort will wrap 10 third-party assemblers as individual
narrative methods using the SDK tools. These methods will allow users
to assemble microbial isolates and small metagenomes using short reads
and in some cases long noisy reads from the third generation
sequencing platforms (PacBio, Oxford Nanopore). Users will also be
able to compare the different assemblies of the same data set using
sequence comparative methods (dnadiff and whole genome alignment)
proposed in the comparative genomic campaign. 

+ Team lead: Fangfang

+ Team: Chris Bun, Moe Alkhafaji

### Description

While many tools have been developed by the genomics community to
produce useful assembly, there is a high degree of variability among
the results of these tools. Competitive evaluations such as
Assembalathon have shown that there is not a single perfect assembler
for all situations. Instead, assembly performance depends heavily on
the characteristics of data set and genome structure. Therefore, we
propose to add a variety of assemblers so that users can explore them
on their own dataset. This effort will also demonstrate the ease and
power of the KBase SDK framework for integrating third-party tools.

The 10 assemblers we will wrap are listed below with a short
description of the relative strengths.

+ A5. A5-miseq is an updated version of the original A5 microbial assembly pipeline. A5-miseq is good for high-quality microbial genome assembly and does so without the need for parameter tuning on the part of the user. It is an integrated meta-assembly pipeline consisting of the following steps and tools: (1) Read cleaning with Trimmomatic; (2) Error
correction with SGA; (3) Contig assembly with IDBA-UD; (4) Crude scaffolding with SSPACE; (5) Misassembly correction based on read mapping using BWA; and (6) Final scaffolding with stringent parameters reparing previously broken contigs.

+ A6. A6 is an Argonne modified version of the original A5 microbial assembly pipeline created by Aaron Darling's group. A5 is good for high-quality microbial genome assembly and does so without the need for parameter tuning on the part of the user. It is an integrated meta-assembly pipeline consisting of the following steps and tools: (1) Read cleaning with TagDust; (2) Error correction with SGA; (3) Contig assembly with IDBA-UD; (4) Crude scaffolding with SSPACE; (5) Misassembly correction based on read mapping using Bowtie; and (6) Final scaffolding with stringent parameters reparing previously broken contigs. A6's modifications over A5 include a bug fix in detecting Phred64 quality coding and replacing IDBA with IDBA-UD for improved assembly accuracy and stability.

+ IDBA-UD. IDBA-UD is an iterative graph-based assembler for single-cell and standard short read data. IDBA-UD is an extension of IDBA algorithm and is good for data of highly uneven sequencing depth. In its assembly process, IDBA-UD iterates from small k to a large k. In each iteration, short and low-depth contigs are removed iteratively with cutoff threshold from low to high to reduce the errors in low-depth and high-depth regions. This iterative approach compensates for the information loss with de bruijn graphs constructed using a single kmer length. For this reason, IDBA-UD is considered one of the more accurate microbial assemblers.

+ Kiki. Kiki is a fast, parallel microbial and metagenomic assembler. Kiki uses a hybrid of the overlap-layout-consensus strategy and greedy contig extension. The overlap-layout-consensus step provides a view of the greater neighborhood of the seed contig graph on which the extender can make more informed decisions about which path to traverse and extend. Compared to de-Bruijn graph-based methods, this approach allows less information loss without the need for chopping reads into shorter kmers.

+ MaSuRCA. MaSuRCA is a short read assembler that combines the benefits of de bruijn graph and overlap‐layout‐consensus assembly approaches. The main concept is the creation of super-reads which contain sequence information present in the original reads. These super-reads are then extended in both directions using an efficient kmer lookup table. MaSuRCA leverages components from the Celera Assembler workflow and other modules such as Jellyfish for preprocessing. Users are encouraged not to preprocess Illumina data before providing it to MaSuRCA as that might cause the assembly accuracy to degrade. Although not currently supported in our wrapper due to resource constraints, MaSuRCA is one of a smaller set of assemblers biologists use for eukaryote assembly.

+ MEGAHIT. MEGAHIT is a single node assembler for large and complex metagenomics NGS reads, such as soil. It makes use of succinct de Bruijn graph (SdBG) to achieve low memory assembly. MEGAHIT is fast and especially suitable for assembly of small metagenomes, metatranscriptomes or low-coverage data in general.

+ MiniASM. MiniASM is an ultra-fast overlap-layout-consensus based de novo assembler for noisy long reads developed by Heng Li. It has been shown to assemble ~50X microbial PacBio reads into a draft assembly of a small number of (sometimes 1) contigs in a matter of minutes. MiniASM derives this performance from a locality-sensitive hashing based overlapper implemented in minimap.

+ Ray. Ray is parallel, graph-based microbial and metagenomic assembler. Ray improves on the vanilla de bruijn graph based algorithm in several aspects: (1) Ray does not stop contig-buiding at the unitigs; rather, it employs greedy heuristics to extend paths. (2) Ray keeps track of the reads from which the k-mers came from and the read pairs from PE reads. (3) Ray uses a repeat removal algorithm inspired by SPAdes.

+ SPAdes. SPAdes is a single-cell and standard assembler based on paired de Bruijn graphs. SPAdes is considered one of the most accurate microbial assemblers and is being actively maintained. SPAdes employs multisized de Bruijn graph which detects and removes bubble and chimeric reads. It estimates insert distance from paired kmers and computes contigs based on  paired assembly graph. Because of the core iterative approach using multisized de Bruijn graph and the innovations in heuristics for error correction (BayesHammer), scaffoding (rectangular graph-based algorithm) and assembly polishing (BWA) that have been perfected over the years, SPAdes has become a top choice for many biologists. Besides, some users have found success in applying SPAdes assembly to very-low-complexity metagenomes (samples with 2-5 species).

+ Velvet. Velvet is a classic de-bruijn graph based assembler. Velvet works by efficiently manipulating de Bruijn graphs through simplification and compression. It eliminates errors and resolves repeats by first using an error correction algorithm that merges sequences together. Repeats are then removed from the sequence via the repeat solver that separates paths which share local overlaps. Velvet is fast and robust, although it's no longer in active development.

The wrapping of these assemblers will leverage the plugin framework in the ARAST assembly service. This means the execution will happen on a dedicated assembly server which sidesteps the current limitations with computational resources of the SDK containers. Only the list of parameters curated by ARAST will be exposed for each assembler. 

### User stories

+ User Jared uses MiniASM to assemble his E. coli strain sequenced with PacBio in 10 minutes and gets a draft genome with only one contig.

+ User Maria tries multiple assemblers (SPAdes, A6, MaSuRCA, IDBA-UD) on the same dataset and compares the reference genome with the 4 versions of assemblies using the dnadiff app to get a sense of which assembly is the closest to the reference.

### Timeline 
+ January 5: deploy a prototype of the SPAdes assembler
+ January 15: deploy prototypes of microbial isolate assemblers: A5, A6, IDBA_UD, Velvet, MaSuRCA
+ January 25: deploy prototypes of assemblers capable of handling small metagenomes: Ray, Kiki, MEGAHIT
+ February 5: deploy a prototype of a long read assembler: MiniASM
+ February 15: explose the logs of assembly execution
+ February 25: promote the wrapped assemblers to beta 

### Test Plan

We will test each wrapper assembler internally with simulated and real
datasets. We will also attempt to get feedback through user testing
from biologists and bioinformaticians on the quality of assembly on
their own datasets.

### Future work

The execution model of these third-party assemblers will be flattened in the next release. This means the assemblers will run on the containers instead of a centralized assembly server. This will require SDK to support large-memory nodes (256 GB+). It can potentially simplify the queuing system and resource allocation. 

