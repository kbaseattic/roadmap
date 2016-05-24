## Ontology Search and Enrichment Services in KBase

### Summary
Implementation of enrichment services based on standard ontologies such as GO for features generated from expression and comparative genomics pipeline.

### Story/Description
RNA-SEQ, TN-SEQ, and comparative genomics all produce sets of "related" genes as key "results" of analyses. A core methodology for adding value to these sets is detection of enrichment of features common to these genes. Popular and important features are those that are assigned by standard ontologies such as GO. Methods such as Fisher’s exact tests are used to determine enrichment of such features in subsets of genes from a genome. We will develop the framework for these based on the new ontology service and an initial set of enrichment tests along with visualizations of results. The ontology service will be key to many future analyses in KBase. This is a natural follow-on to a number of core functions we need to add to the system or that will come-in via the SDK.

 User provides a list of genes to be analyzed and select the name of the species and type of the ontology (cellular content, biological process or molecular function). The external gene IDs associated with genes must be supported by KBase (GenBank, EBI, Phytozome  etc). If the genome doesn’t exist, you can alternatively provide the Gene IDs and associated GO accessions. The user can also select the significance level based on one of the three statistical test methods - hypergeometric, chi-square and fisher test. In addition, user can choose one of the methods such as Bonferroni, Hochberg, Hochberg (FDR), Hommel, Holm etc. to do the multi-test adjustment.

The result will be table that displays a list of GO terms with enrichment scores, the sample frequency, the background frequency and the adjusted p-values. Sample frequency will be the number of genes those were annotated with GO term whereas the background frequency will be the number of genes annotated to a GO term in  the GO-full or GO-slim set. The results could also be visualized as bar chart or color-coded GO hierarchy in the output widget. For GO visualization details, please see this image (incl. statistically significant GO terms): http://journals.plos.org/plosone/article?id=10.1371/journal.pone.0079011#pone-0079011-g016 

### Use Cases:
1. User queries for gene model(s) in a species and all ontology terms associated with the gene model(s) are returned. This could be used for Gene ontology enrichment analysis to find which GO terms are overrepresented or underrepresented using annotations for that gene list.

2. GO enrichment studies can be applied to the candidate genes obtained from GWAS studies and Expression profiling studies to see the enrichment of the biological functions associated with those candidate genes. Users can also search the candidate genes based on the terms associated with “Cellular content”, “Biological Process” and “Molecular Functions”. 

3. GO enrichment studies can be used to identify biologically meaningful coexpression clusters (functional modules) and thus helps users to identify biological pathways associated with the related biological process of the genes of interest. 

### Dependencies
1. Genome with features with GO term association as aliases
2. Background reference annotation (GO full or GO slim for each species)


### Timeline
~2 sprints

