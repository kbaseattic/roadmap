Reference Data Value Added Pipeline
=========================================

### Summary

This product builds on the momentum we've gained in reference data in Q2, integrating SDK fully into the reference data pipeline and adding significant additional value to our standard processing pipelines for genomes and ontology. Simultaneously, we will build a fully extensible general pipeline for managing and processing all reference data in KBase.

### Extended description

During the Q2 ontology and reference data sprints, we have established a pattern of operations that are commonly performed on reference data of all types as the data is integrated into KBase. Typically, the data is downloaded periodically from an online source in some file format (or combination of files), then the files are submitted to a pipeline that: (i) validates the file (or files) and reports failures; (ii) converts the file (or files) into a KBase typed object; (iii) saves the typed object into one or more public reference data workspaces; (iv) runs a variety of value-add processes on the object such as genome annotation, standardization, or mapping; and (v) indexes the object in SOLR. While this process has been automated for some example reference objects (e.g. genomes from ref-seq), these reference data pipelines is still constructed in a highly customized way on a per object basis. This makes the ongoing maintenance, extension, update, and upgrade of our reference data a challenge.

We have two goals for this product:
1.) Construct a fully extensible pipeline for managing, updating, and standardizing reference data. Essentially, one should be able to specify the following series of operations to load new reference data (or maintain existing reference data) in KBase: (i) a process for downloading the latest copy of data; (ii) a process for converting data into KBase types and saving to a reference workspace (exploiting current data-to-files work); (iii) a series of standard analyses to run on the object (e.g. RAST anntotation, interpro2go, and protein domain analysis for a genome); and (iv) a process for indexing objects for search. 

All components of the pipeline would be modular and could be updated and maintained independently. Ideally these would be operations encoded within SDK modules. Likely there would need to be some notion of versioning so an updated version of the pipeline could be re-run on all reference data as needed. This pipeline should have the capacity to run the SDK processing steps in massive batch mode in order to process tens-of-thousands of genome objects.

The pipeline would maintain reports on the results of every integrated reference data object, including full provenance for each object, and any data/errors reported by any step of the pipeline processing each object. The system would also record which version of each processing step ran on each object, which would facilitate updating of data when the pipeline is altered.

2.) Apply the constructed pipeline to extend our current reference data pipelines for genomes and ontology, as well as adding a pipeline for biochemistry. For genomes, we would extend the pipeline to include several value-addition steps, including:
-   loading genome meta data (e.g. reference strains, hosts, environments)
-   RAST annotation
-   Conserved domain computation
-   Recruiting to species tree
-	Assigning all proteins to families
-   Computing signatures in proteins
-   Constructing metabolic models
-   Running FBA to compute example flux, minimal media, and essential genes
-   Gapfilling
-   Linking genome to ontology

For biochemistry, we would load reference databases in biochemistry, making compounds and reactions first class objects with landing pages. We could map this data to the models built for genomes in the genome pipeline.

For ontology, this would be about continuing the efforts at crosslinking ontology to other reference data (e.g. genes, compounds, reactions, model, genomes, genome metadata) that we began doing in Q2.

We would need to extend the typed objects for genomes to include additional data created by the new added value steps that we add, but this would be well worth the effort. This would include domains, competing ontologies, protein families, reactions, EC numbers, and pathways possible added to genes in genomes. We would also create a systematic gold-standard pipeline that it might be possible to make easily accessible to users to run on their own genomes.

### Timeline for feature release

**Sprint 1:**

-   Convert all steps of existing genome and ontology pipelines to SDK
-	Construct prototype SDK operations pipeline and demonstrate by stringing together genome operations
-	Mockup UI for constructing and extending a reference data operation pipeline, as well as viewing pipeline output

**Sprint 2:**

-   Refine prototype SDK operations pipeline
-   Prototype UI for viewing output from running the value add pipeline to load reference data
-   Prototype UI for building and altering the pipeline (e.g. registering new steps in a pipeline)
-   Add 3-4 added value steps to the genome pipeline
-   Build prototype biochemistry pipeline

**Sprint 3:**

-	Complete adding added value steps to the genome pipeline
-	Add added value steps to ontology pipeline
-	Complete biochemistry pipeline
-	Extend SOLR scheme to include additional data from added value steps

**Sprint 4:**

-	Refine landing page for genomes to include added value data
-	Refine landing page for ontology to include added value data
-	Create landing pages and search pages for biochemistry

### User stories

1. A user notices something strange with a reference genome in KBase. They view the added-value provenance data for that genome and learn that a step failed due to extremely poor quality contigs.
2. Users can see and download domains for any protein of any reference genome in KBase.
3. User queries the reference genomes to find key model strains based on our reference data.
4. User identified all genomes and genes associated with a specific reaction or pathway of interest.