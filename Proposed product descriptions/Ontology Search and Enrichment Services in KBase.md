## Ontology Search and Enrichment Services in KBase

### Summary
Implementation of enrichment services based on standard ontologies such as GO for features generated from expression and comparative genomics pipeline.
Data types: Ontology Index, New version of Genome

### Story/Description
RNA-SEQ, TN-SEQ, and comparative genomics all produce sets of "related" genes as key "results" of analyses. A core methodology for adding value to these sets is detection of enrichment of features common to these genes. Popular and important features are those that are assigned by standard ontologies such as GO. Methods such as Fisher’s exact tests are used to determine enrichment of such features in subsets of genes from a genome. We will develop the framework for these through development of an ontology service and an initial set of enrichment tests along with visualizations of results.

The ontology service will be key to many future analyses in KBase. This is a natural follow-on to a number of core functions we need to add to the system or that will come-in via the SDK.

Types of Ontology: Standard ontologies such as GO, plant ontology (PO), trait ontology (TO), environment ontology (EO), microbes environment ontology (ENVO) etc. These ontologies can be periodically transferred from their respective parent sources into a dedicated workspace. Transfer should be automatic. 

User selects the genome name and provides a list of genes. The external gene IDs associated with genes must be supported by KBase (GenBank, EBI, Phytozome  etc). If the genome doesn’t exist, you can alternatively provide the Gene IDs and associated GO accessions. The user can also select the significance level as well as the type of multi-test adjustment that can be applied such as Bonferroni, etc.

The result will be list of GO terms with enrichment scores as adjusted p-values. It could also be visualized as color-coded GO hierarchy in the output widget.



### Use Cases:
1. User queries for gene model(s) in a species and all ontology terms associated with the gene model(s) are returned. This could be used for Gene ontology enrichment analysis.
2. Ontologies should be searchable. User could search with text like “Lignin content” and the ontology service should be able to tell if there is a trait ontology term associated with this trait.
3. User wants to search for all GWAS studies that have phenotype “lignin content” as part of their assay. 
4. User wants to search for all RNA-seq experiments based on tissue, developmental stages or treatment. eg. chemical treatment, abiotic stress treatment or biotic stress.
5. User wants to construct a co-expression network based on tissue or treatment. eg. abiotic stress related co-expression network and hub genes.


### Dependencies
1. New Genome TO and loaded Genome in KBase
2. KBase synchronous service for Ontology graph loaded in KBase (Without it, it still can be done)
3. KBase ontology search


### Timeline
3-4 sprints (2-3 sprints if we implement enrichment part only or 3-4 sprint if we have to implement search service)

