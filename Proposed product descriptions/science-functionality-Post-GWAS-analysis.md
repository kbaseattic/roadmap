## SDK and Science Target Functionality - post GWAS functional analysis

### Summary
The methods in this service will help users to explore Genomewide association analysis results, multiple ways to visualize the results, integrate with omics datasets, expedite data mining and aid hypotheses building.

### Story/Description
Genome wide association analysis (GWAS) identifies statistically significant single nucleotide polymorphisms (SNPs) related to phenotype / trait of interest. Post GWAS analyses which is going from list of SNPs to a more complete biological story is a major bottleneck. Most of these analyses require manual data extraction and integration with other data types including expression data and pathway data. Just sharing of this dataset is a big challenge for the community.

GWAS populations and thousands of population level measurements are available for various plant species including Arabidopsis, Populus, Medicago, Sorghum, Maize, Soybean, Foxtail millet, Rice, Switchgrass etc. It is a new functionality and will help us target a different set of researchers leading to publications and citations.

There are not many publicly available data sources for gwas datasets. Engaging community members and allowing easy ways to upload these datasets and their integration will enrich the KBase knowledgebase component. Sequenced genomes contain thousands of unknown genes and a proper integration of gwas datasets will help build hypothesis on function of unknown genes.

This product will have following methods.

#### Data types and uploader methods

    upload SNPs
    upload SNP statistics for each phenotype
    upload phenotype data
    upload population metadata (eg. latitude, longitude, climate, soil)
    upload expression data (already implemented)
    upload network data (not defined yet?.. Something for future)
    
    
#### Supported narrative methods in the short term

Mockup narrative here: https://appdev.kbase.us/narrative/ws.179.obj.1

    Associate SNPs to a genome
    Display GWAS results
        static manhattan plot
        Interactive manhattan plot
        QQ-Plot
        Box plot distribution of phenotypes
        Phenotypic values displayed on world map
    Identify gene list corresponding to SNPs
    Calculate and View LD in a region of the genome
    Gene score analysis
    Pathway enrichment analysis
    Identify common SNPs and genes across multiple related phenotype categories
    Associate genelist to expression data and visualize as heatmap
    Associate gene list to user uploaded network data (Dependency network data uploader)
    Gene ontology enrichment analysis (part of GSEA PD)
    
#### Supported narrative methods with external dependencies (longer term)

        Visualize SNPs in genome browser
        Predict functional effect of SNP (SIFT , snpEFF etc.)
        Analysing non-coding SNPs by associating it to a database of conserved non-coding sequences and regulatory motifs


### Use cases
Researcher A has completed genome wide association analysis for drought tolerance in Sorghum. GWAS is done outside of KBase. She imports genotype/phenotype/gwas_results to KBase using import methods. The GWAS results show that she has 100 SNPs that are significantly associated to the phenotype. She also has other omics datasets related to drought stress. She wants to understand the biology and underlying genes/pathways that she can then use to engineer plants for drought tolerance.
    
#### Time line

The initial effort is focused on getting the data models correct, outreach with community members and finding right set of data sets and methods.

##### Sprint 1-4:
- Develop data models to support genotype/phenotype datasets.
- Support for phenotype ontology
- Identify key community members and work with them to get publicly available GWAS datasets into KBase
- Identify and engage users working with different genomes to find gaps/methods needed
- Initial set of backend methods / visualization methods to engage the community

##### Sprint 5-8:
- Enhance backend methods / visualization methods
- Search and integration of publicly available gwas datasets


### Test Plan
Potential users from different communities will be engaged right from the first sprint. They will upload test/real datasets and give feedback on the methods.



