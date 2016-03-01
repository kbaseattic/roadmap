#Homology Search Service Product Description

##Summary
The homology search service will enable a user to rapidly query a database of protein sequence data stored in the KBase database for an input set of protein sequences. The service will ultimately support a variety of global NRs compiled from numerous data sources, and it will support queries against user-uploaded sequence data as well. The homology search functionality will be available in two places: (i) the search page on KBase.us, accessible without a KBase account; and (ii) as a method in the KBase narrative. On the search page, users will be able to paste in one or more protein sequences. The search will run on the fly, and results will appear on screen as a table of homologous genes found for each query sequence. Users will be able to select results and either: (i) download in FASTA or TSV format, or (ii) copy into an existing narrative as an object. In the narrative, the user can upload a fasta file as a feature set, or they can search for features in the search page and copy to a narrative as a feature set. Users can then run the “Protein Homology Search” method using either a feature set or direct sequence data as input. Users will be able to select an NR, set search parameters, and then run the search a-synchronously. Results will appear and be viewable in the narrative in a variety of formats.

+ Team lead: Maulik

+ Team: Maulik, Fangfang, Harry (UI), Bob O.

##Extended description
The proposed “Homology Search Services” are designed to allow a user to search for homologous proteins for a query sequence in a variety of data-sources in KBase, including: (i) user genomes; (ii) reference genomes in KBase; and (iii) a set of external data NRs. The service will return lists of homologous proteins and sequence alignment parameters, with speed depending on the search algorithm selected. This is immediately useful to users who simply want to use KBase to get a list of homologs for a gene of interest. However, the primary goal of this service is to facilitate the exploration of potential protein function, which has greatly influenced our design of peripheral support methods for the homology-search user experience. A detailed timeline of all planned features is provided in the following section.

A key detail in this proposed service is the NRs that will make available for query by the homology service, as well as how we will make the NRs available to the user. The user will always have access to a set of global NR databases that will be maintained by the KBase reference data team. Critically, these global NRs will contain no user data. Initially, the only global NR we will provide will be comprised of all proteins included in the reference genome database for KBase, including plants and microbes. Over time, additional global NRs will be added, including useful subsets of the KBase NR (e.g. plants) and extensions of the KBase NR to include external databases (e.g. NCBI). Ultimately, protein sequences from metagenomics databases could also be added to a global NR, but this is a long-term goal. All global NRs will be maintained by the KBase reference data team (Maulik, ?). For the initial KBase global NR, an automated script will be set up to maintain this NR as a part of the reference database update process.

Currently, Ranjan has developed a homology search tool that operates against user data, which is currently deployed into https://narrative-ci.kbase.us/. We are proposing to ultimately subsume this tool into our own homology search method. Our goal is to allow users to select any of the three following object types as additional possible NR for homology search (besides the global NRs, which will always be available): (i) genome; (ii) feature_set; and (iii) genome_set. Our design will deviate from Ranjan’s design in that the compilation of NRs from sequence data will not take place in a separate step in the narrative, but rather be integrated into the "Homology search" method itself. We do this for: (i) simplicity, (ii) because some algorithms don't require compiled NRs, and (iii) because compilation of NRs is relatively fast. Generally however, our proposed "Protein homology search" method will have essentially the same inputs as Ranjans method, including: query sequence as plain text or as a selected genome or feature_set; selected NR; homology search algorithm; or homology search parameters.

The "Protein homology search" method will produce a new output object, which will build on the object type used by Ranjan's blast method [GenomeUtil.BlastOutput‑4.0](https://narrative-ci.kbase.us/functional-site/#/spec/type/GenomeUtil.BlastOutput-4.0), and we will utilize many of the same viewers that Ranjan developed. 

A homology search on it's own in isolation will not necessarily mesh well with the ecology of tools already present in KBase. Thus, we also plan to provide a body of support methods to enable the use of homology hits either directly to understand the function of a protein (by looking at the functions annotated to the homologs), or to use trends in the context of the homologous genes to identify function (by looking at functions that are repeatedly associated with genes that are co-localized with the homologous genes).

One potential follow-up analysis that we envision applying to the output of the "Protein homology search" method is multi-sequence alignment, but this workflow should be described in a separate product description. What we do propose to build in the context of this product description is a series of tools to view the functions and contexts of the homologous genes identified by the "Protein homology search" method. First would be a method that builds a profile of the functions represented among the homologs identified by the search. This would highlight which functions are most commonly represented among the homologs (and are thus potential functions for the queried protein). This tool will operate on any source of annotated functions, although the approach will work best when functions are from a consistently applied annotation ontology. A second proposed method would be a simplistic "compare regions" view similar to that available in [SEED](http://pubseed.theseed.org/?page=Annotation&feature=fig|1148.72.peg.2809). This view will show the regions of the chromosome surrounding each homologous genes, with isofunctional genes consistently colored to easily show where functional clusters occur on the genome. This function will also provide the distribution of functions commonly colocalized with identified homologous genes, providing further clues for the functional context of the query protein. We also envision the output of the "Protein homology search" method feeding into: model gapfilling, co-expression analysis, and variation analysis.

##Timeline for feature release
+ January 19: deploy a prototype of the homology search backend and the sequence search page into narrative-ci
+ January 19: deploy a NR for KBase reference genome database
+ February 5: deploy homology search service and sequence search page to production
+ February 5: deploy a prototype of the "Protein homology search" method and "Distribution of represented functions" method to narrative-ci
+ February 19: deploy a prototype of the "Compare gene regions" method to narrative-ci
+ February 26: deploy "Protein homology search" method, "Distribution of represented functions" method, "Compare gene regions" method to production

##User stories
+	User Gyorgy comes to the KBase home page. He queries on the main search page for “thermotoga cellulose”. He selects one of the genes that comes up, opening up the gene page and copying the protein sequence. He then selects “sequence search” and pastes the protein sequence. He gets a list of homologous genes, which he copies to a narrative and then exports and downloads as a fasta file. He uses the homologs to attempt to find a version of a gene he can express in E. coli for protein crystallization.

+	User Chris runs a metabolic model and finds a dead end pathway consisting of ten steps, only one of which is present in his genome. He selects the gene in the model viewer and exports it to his narrative as a feature set, which he labels “orphan protein”. He then selects the homology search method, enters in his “orphan protein” object, hits submit. The results pop up. He looks in the functional distribution and finds that many of the homologs are annotated with a different role than the original orphan protein. Furthermore, that role is associated with a gapfilled reaction in his model. Chris then looks at the functional context analysis, which shows that his protein has a context that is much more consistent with this gapfilled function than with the original function. Chris reannotates the protein and rebuilds the model.

##Narrative mockup
https://narrative-ci.kbase.us/narrative/ws.3594.obj.1

##Search mockup
<center>
<img src=https://raw.githubusercontent.com/kbase/roadmap/master/images/homology_search_search_mockup.png  alt="Search mockup" style="height: 600px;"/>
</center>
<br/>

##Citations to code sources
+ BLAST

+ DIAMOND

+ Kmer-based search (SEED)
