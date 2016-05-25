## Ontology Support Services - ANL

### Summary
Implement a set of datatypes and tools to support the storage, access, query, and comparison of ontologies, as well as the mapping of ontologies to a genome (where appropriate).

### Story/Description
Ontologies are everywhere in biology. We use them to describe where a genome was isolated, the conditions of an experiment, a tissue in a plant, the function of a gene, the class of activity of a related set of genes, or a metabolic pathway. If we could handle ontology data properly in KBase, it would support the use of diverse ontologies for: (i) creating consistent and query-able metadata; (ii) gene enrichment analysis; (iii) comparison and remapping of different annotation sources; and many other diverse and powerful applications. 

Here we are proposing to build the services and tools that will lay the groundwork for a rich support of ontology in KBase. Specifically, we will: (i) design and populate new workspace data types for ontologies; (ii) expose a search UI for browsing and querying ontology data; (iii) construct and load mappings between ontologies that are associated with similar biological entities (e.g. homologous genes); and (iv) construct tools enabling the assignment of ontology terms to genes in a genome or for remapping a genome annotated in one ontology to a new ontology. We describe these components in more detail below:

#### Core ontology service
Here we are fundamentally proposing to add "ontologies" as a new reference data type in KBase, and we will handle this type in a manner that is analogous to how genomes are handled now. What does this mean? First, we will have a set of reference ontologies loaded into KBase in: (i) a publicly accesible workspace exposed in the "public" tab of Narrative data panel; (ii) a search UI permitting users to search the reference ontologies for terms. The workspace data type will be called "OntologyDictionary", and it will be designed to support different types of ontologies (e.g. environments, tissues, annotations, pathways) in a general way, with ontologies assigned to a category based on the type of entity they map to (e.g. genes, reactions, environments, genomes) and the purpose of the ontology (e.g. experimental description, or description of function). The type will capture full information about the hierarchical organization of ontology terms, as most ontologies involve hierarchical organization. Reference ontologies will be maintained with periodic automatic updates, using the same infrastructure being developed for automated maintenance of genome data. In addition to the ontologies themselves, we will also create and maintain mappings between some of our reference ontologies. These mappings will also be periodically updated and maintained. As we are using workspace to hold the ontology data, we will not need a separate ontology service. Tools constructed to use the ontology data in analysis will be standard SDK modules, exposed via the narrative interface. Also, as the ontologies will be objects in the workspace, we will be creating uploaders and downloaders and landing pages, and users will be able to load their own ontologies if desired. The file format we will support for the ontology dictionary will be "OBO", a common format used for ontologies.

In this initial product, we will focus primarily on gene annotation ontologies, specifically GO and SEED, as these have immediate applications in KBase. But we will also explore the integration of at least one other ontology type (tissue or environment) to ensure our design is not overly limiting to only one ontology type. 

#### Supporting ontology browsing and search
We will index all of our ontology objects in SOLR, and a UI will be constructed for searching this data as an extension of the existing KBase search page. Again, this mirrors the treatment of KBase reference genomes and establishes a nice design pattern for the handling of reference data in KBase. This will require basic landing pages for ontology terms and the ontologies themselves. These landing pages will show the hierarchy, exemplars, and mapped terms for each ontology term.

#### Creating a mapping between multiple annotation ontologies
Here we are proposing to obtain mappings between multiple ontologies from downloaded sources. Specifically, GO provides mappings to unitprot key words, EC, KEGG, and MetaCyc. We will also create a mapping to SEED by re-annotating a diverse reference set of SEED genomes (covering all microbial life) with interpro2go and comparing annotations and constructing a translation table accordingly. We will do the same thing to build a PlantSEED mapping, using all complete plant genomes in that case. Generally, we expect to obtain mappings maintained externally where-ever possible, thereby placing the burden of maintaining these mappings on external projects. We will store all mappings in another KBase typed object in the workspace, which we call an OntologyTranslation. Like the ontologies themselves, we will maintain a public set of maps in a public workspace accessible in narrative, and we will index mappings in SOLR. We will have uploaders and downloaders, and users will have the ability to upload and use their own mappings.

#### Creating initial ontology tools for Narrative
We will expose the ontology functionality in the narrative with a variety of tools. First, we will wrap the interpro2go annotation pipeline in SDK, enabling users to annotate a KBase genome with GO terms based on interpro domains. Second, we will offer a general ontology translation method, where a user can apply any existing ontology map to translate genome annotations from one ontology to another. Third, we will offer a more specific ontology translation which will convert genome annotations to GO based on EC numbers and uniprot key words. Because all ontologies are different, we expect this is the way we will need to go in many cases - creating specific tools to support major ontologies. We would offer more general annotation approaches based on exemplar genes, but we now feel this is probably out of scope and a topic of a future set of sprints. The problem is this work involves too much new science. Better to go with established existing and accepted pipelines for assigning GO terms. We already have pipelines in KBase for assigning SEED and PlantSEED annotations.

### Interactions with the euks team:
The 3 sprints for this proposed work occur at the same time as a sprint from the euk team to support this work. Specifically, the euk team will:

1. Develop use cases to drive typed object design and tool design, and also consult on typed object and tool design.
2. QC/review of loaded ontologies and tools
3. Help build the search UI and landing pages for ontology objects
4. Consult on design throughout via weekly meetings at a minimum to ensure that the service will meet future demands and use-cases (e.g. gene enrichment)
5. Aid in writing tutorials and docs

### Future work:
Some ideas that came up in our brain storming with the euks team for future work on this topic:

1. Develop a tool for doing gene enrichment analysis

2. Ultimately, we need a tool to map ontology terms to transcripts (particularly plant transcripts)

3. We need to know specifically what parts of a sequence led to the assignment of a particular ontology term to a protein (mainly for plants)

4. We could port the interpro-to-go pipeline for annotating the GO ontology.

5. We could build on the kmer-based annotation technology used by our RAST genome annotation service to annotate other ontologies, in addition to just SEED.

### Use Cases:
1. A user wants to build a model of a GO-annotated plant genome. They translate their GO annotations to PlantSEED (or the model reconstruction service does this internally), and build the model without having to first re-annotate their genome.

2. A user loads RNA-seq data from a variety of plant tissues using the bulk-upload service. The meta-data tool in the bulk upload service accesses the tissue ontology (TO) in the ontology service and enables users to specify the tissue for each RNA-seq sample from the available TO terms (we like this user story because it connects bulk upload and ontology).

3. A user wants to query the gene models in a species and all ontology terms associated with gene models are returned. User can filter the ontology terms based on the ontology domain (cellular content, biological process, molecular functions) and evidence codes (EXP; IDA; IEP; IMP; IEA etc.)

4. A user wants to search the controlled vocabulary terms. These can be searched by giving keyword, ontology id etc. e.g if a user wants to search “root”, then he should be able to get PO term for “root” tissue using KBase search and can use this term for curation of expression sample metadata. 

5. A user wants to see the enrichment of the biological process or molecular functions associated with the differential expressed genes obtained from RNA-seq pipeline. This PD will help in creating foundation for performing GO and pathway enrichment studies later and various ontology tools can be added as a part of SDK by third party developers. 

6. Mapping of SEED terms with GO will help in identification of key molecular pathways and robust gene ontology signatures when these will be used with methods related to gene expression profiles and metabolic models. 


### Dependencies
We hope to reuse the automated update and maintenance capabilities developed by the reference data campaign at ANL.

### Timeline

#### Sprint 1
1. Design all ontology data types in workspace, and load prototypes for GO, SEED, and PlantSEED
2. Build uploaders and downloaders for ontology data types
3. Build simple prototype ontology landing pages
4. Testing

#### Sprint 2
1. Design SOLR scheme for ontology dictionaries and translations and begin loading
2. Build SDK methods for general translation and for translation based on EC/keywords
3. Compute and load mapping between SEED and GO based on comparing SEED and GO annotations
4. Refine landing pages
5. Testing

#### Sprint 3 
1. Wrap the interpro2go pipeline in SDK and expose in narrative
2. Build ontology search UI
3. Refine work from previous sprints based on feedback
4. Complete automated update infrastructure to maintain reference ontology data
5. Document and test all features
