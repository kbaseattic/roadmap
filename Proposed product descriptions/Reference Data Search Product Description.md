Reference Data Search Product Description
=========================================

### Summary

KBase’s Reference Data Search allows users to quickly find reference
datasets of interest by performing sophisticated keyword searches,
select them, and save copy them to narratives to perform analysis using
various narrative methods.

Currently, searchable reference datasets include public microbial and
plant genomes, genomic features, and metabolic models. This list will be
expanding rapidly as we incorporate more data types into KBase Reference
Data Collection.

Here, we propose several enhancements to improve the usability of the
current Reference Data Search and addition of Biochemistry Data to the
current search.

### Extended description

1.  Save results as genome or feature sets:

    The current reference data search allows users to select genomes or
    features from the search results and copy them to narratives. The
    copied data objects are added to the narrative as individual
    entities, making it difficult to browse, manage and use them in the
    follow up analysis. Often, users want to save the selected search
    results as a genome or feature set that can be used as input in the
    other comparative analysis methods available in KBase, such as
    construction of pan-genome, or building MSA and tree for a set
    of features.

    To enable this, we will enhance the current reference data search
    interface to allow users to select one or more genomes or features
    and save them as a genome or feature set in the narrative. The users
    will be able to incrementally add more items to the existing sets
    and grow them over time.

2.  Biochemistry data:

    We have developed new Solr schema to load reference biochemistry
    data dictionaries for metabolic compounds, complexes, reactions and
    roles, and subsystems. We propose to make the same data types
    searchable using the reference data search interface.

    We will also create data landing pages for each of the data types,
    which will provide more information about the data and will be
    linked from the search results.

3.  Reference Data Solr Schema Enhancements:

    We propose the following enhancements to the existing Solr schema to
    provide better search experience to the users.

-   **Search logic:** While searching for reference data using multiple
    keywords, user AND as the default search logic, instead of using OR.
    For example, currently if a user searches for *Escherichia coli HS*
    using reference data search, 2339 genomes are returned, as they
    match Escherichia OR coli OR HS. These represent too many false
    positive matches and something not expected by the user. However, if
    AND is used as the default search logic, it returns only two
    matching genomes, which is exactly what user expected.

-   **Genome metadata:** Genome metadata refers to the descriptive data
    about a genome, which provide additional information about the
    genomes, such as genome status, sequencing platform and depth,
    isolation source, geographic location, host, collection date, other
    clinical or environmental factors, phenotype related information,
    and cross references to external databases, such as NCBI’s
    BioSample, BioProject, Assembly, GenBank, and SRA database.

    As there are hundreds (or sometimes even thousands) of genomes
    sequenced for the same species and strain, metadata is absolutely
    crucial to distinguish one genome from another and understand why
    the genome was sequenced. Often, filtering the genome based on
    available metadata is essential first step to identify a set of
    genomes one wants to include in comparative genomic analysis. For
    example, a user may want to select Brucella genomes isolated from
    different hosts and compare them using pan-genome tool to understand
    host-specific adaptations.

-   **Value added annotations:** One of the objectives of the KBase
    reference data ingestion process is to annotate all the microbial
    genomes using a consistent vocabulary and also provide value added
    annotations, such annotation of protein families, domains, and
    operons, which provide rich source of information and form the basis
    of many comparative genomic analysis methods. As we ad support for
    value added annotations in the KBase genome annotation method, we
    will also incorporate them into the object models, Solr schema, and
    the reference data search.

### Future work

1.  Enhance data landing pages for genomes and genomic features.

-   Display genome metadata, db xrefs with linkouts

-   Display additional feature annotations

### 

### Timeline for feature release

**Sprint 1:**

-   Select genomes and genomic features from search results and save
    them as genome or feature sets.

**Sprint 2:**

-   Add biochemistry data to reference data search

-   Design and develop data landing pages for the biochemistry data
    types

**Sprint 3:**

-   Extend Solr schema and WS data object models to support genome
    metadata and value added annotations

### User stories

### 

### Narrative mockups
