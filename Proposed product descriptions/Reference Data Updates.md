Reference Data Updates (ANL): Expanding reference data to include RefSeq, Ensembl, and Phytozome
=========================================

### Summary

Here we propose to expand the reference genomes in KBase to include RefSeq, Ensembl, and Phytozome.

### Extended description

This produce involves making all genomes in RefSeq, Ensembl, and Phytozome available for immediate use in any narrative, as well as making these genomes searchable via the KBase search interface. Genomes will be available in their native forms, with native gene IDs and functional annotations.

1. Public workspaces will be created which will house the latest copies of all RefSeq, Ensemble, and Phytozome genomes (in separate public workspaces) as genome typed objects (both the current version and possible the new version if necessary data API support is available) 

2. All genomes will be available for copy into any narrative via the "public" tab in the narrative data panel. Each genome source will be available in a separate category on this tab (e.g. RefSeq genomes, Ensemble genomes, Phytozome genomes, KBase genomes). 

3. These genomes will be stored in their native form, with original gene IDs, gene calls, and functional annotations.

4. All genomes will be loaded into the KBase SOLR with some scheme modifications to support the genome data, and genomes will searchable via the KBase search interface. Users will preselect which genome source they want to query in the search.

5. Support will be added for the automated maintenance of this so the KBase copy of this data stays synchronized with RefSeq, Ensembl, and Phytozome).

6. Logic would be added to the KBase modeling pipeline to throw an error if a user attempts to build a model of a RefSeq genome without first re-annotating the genome with RAST. Possibly, depending on how the ontology sprints are proceeding, we could explore automatically re-mapping RefSeq annotation to RAST.

### Future work

1.  Update the KBase reference genomes by running all of the RefSeq, Ensembl, and Phytozome genomes though a standard KBase processing pipeline, where we will assign KBase IDs to all genes and genome, we will recall genes in all RefSeq genomes, and we will re-annotate all RefSeq genomes with RAST.

### Timeline for feature release

**Sprint 1:**

- Retrieve microbial genomes from RefSeq and plant genomes from Ensembl
- Design scripts to load genomes (as GenBank files) into workspace and index them into solr
- Load a small batch of test genomes (~100-200) and make any changes needed in the existing upload scripts and/or Solr schema to capture data source and provenance.
- Evaluate performance for loading large batches. 

**Sprint 2:**
- Start loading microbial genomes from RefSeq and plant genomes from Ensembl.  
- Develop scripts for loading plant genomes from Phytozome, which will require first creating GenBank files from FASTA and GFF files
- Design automatic genome update pipelines v1: minimally for RefSeq, and if time, Enseml and Phytozome as well

**Sprint 3 (not a full sprint - mostly UI person):**

- Refind and complete automatic update pipelines for all sources
- Finish loading any remaining genomes
- Enable use of KBase search and narrative data panel to query and select RefSeq, Enseml, and Phytozome genomes
- Refine search UI based on feedback

### User stories

1. User searches for and identifies a specific RefSeq strain for which they have experimental data, copies the strain to their narrative with native gene calls intact, and loads their data and links to the strain.
2. User attempts to build a model of a genome with RefSeq annotations. An error is thrown indicating that the genome should be annotated prior to model reconstruction.

### Narrative mockups
