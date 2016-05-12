Reference Data Value Added Pipeline
=========================================

### Summary

We propose to take what we've learned and built between the Q2 reference data/ontology sprints and the SDK effort to construct a fully extensible pipeline for managing and processing reference data.

### Extended description

During the Q2 ontology and reference data sprints, we have established a pattern of operations that are commonly performed on reference data of all types as the data is integrated into KBase. Typically, the data is downloaded periodically from an online source in some file format (or combination of files), then the files are submitted to a pipeline that: (i) validates the file (or files) and reports failures); (ii) converts the file (or files) into a KBase typed object; (iii) saves the typed object into one or more public reference data workspaces; (iv) runs a variety of value-add processes on the object such as genome annotation, standardization, or mapping; and (v) indexes the object in SOLR. While this process has been automated for some example reference objects (e.g. genomes from ref-seq), these reference data processing pipelines is still constructed in a highly customized way on a per object basis, and the pipelines are not easily extensible or upgradable. This makes the ongoing maintenance, extension, update, and upgrade of our reference data more of a challenge than it should be.

KBase requires a fully extensible pipeline for managing, updating, and standardizing reference data. Essentially, one should be able to specify the following series of operations to load new reference data (or maintain existing reference data) in KBase: (i) a process for downloading the latest copy of data; (ii) a process for converting data into KBase types and saving to a reference workspace; (iii) a series of standard analyses to run on the object (e.g. RAST anntotation, interpro2go, and protein domain analysis for a genome); and (iv) a process for indexing objects for search.

All components of the pipeline would be modular and could be updated and maintained independently. Ideally these would be operations encoded within SDK modules. Likely there would need to be some notion of versioning so an updated version of the pipeline could be re-run on all reference data as needed. 

Once created, the pipeline would include specifications for how often it should run to update reference data. 

The pipeline would maintain reports on the results of every integrated reference data object, including full provenance for each object, and any data/errors reported by any step of the pipeline processing each object. The system would also record which version of each processing step ran on each object, which would facilitate updating of data when the pipeline is altered.

We propose to build this pipeline and migrate our current reference genome and ontogoloy pipelines to this system. We will also use the pipeline to extend our genome annotation reference data process to include RAST annotation as a step in the process for all reference genomes (although we will not necessarily overwrite existing annotations with RAST annotations - likely we will store these separately).

### Timeline for feature release

**Sprint 1:**

-   Convert our SOLR indexing scripts into SDK modules
-	Convert our genome/ontology download and update operations to SDK modules
-	Mockup UI for constructing and extending a reference data operation pipeline, as well as viewing pipeline output

**Sprint 2:**

-   Construct prototype SDK operations pipeline and demonstrate by stringing together genome operations
-   Prototype UI for viewing output from running the value add pipeline to load reference data
-   Prototype UI for building and altering the pipeline (e.g. registering new steps in a pipeline)

**Sprint 3:**

-	Implement the ontology and genome reference data update pipelines fully in new system
-	Finalize UI for viewing pipeline output
-	Finalize UI for managing the pipeline

### User stories

1. A user notices something strange with a reference genome in KBase. They view the added-value provenance data for that genome and learn that a step failed due to extremely poor quality contigs.
2. Users request that domains be computed for all reference genomes in KBase. We add the domain computation to the reference pipeline, and we edit the indexing step of the pipeline to add the domain data to SOLR. We apply the changes, which automatically runs the new and altered processing steps on all genomes (but does not re-run annotation).
3. Users request published models from the BIGG database to be added to the reference data. We quickly piece together a new pipeline to sync with the BIGG database, download models in SBML, transforming to KBase models, running gapfill, and running FBA on all models.
 
### Narrative mockups