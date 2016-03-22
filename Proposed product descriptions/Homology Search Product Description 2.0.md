Homology Search Product Description
===================================

### Summary

The Homology Search service will enable a user to rapidly query KBase
public reference genomes and genomic features using DNA or protein
sequences and find matching genomes, genes or proteins, and select
results and save them as genome or feature set in a narrative.

The homology search functionality will be available in two places:

1.  The Reference Data Search page KBase.us, which will be accessible
    without login
2.  As Homology Search Method from the KBase narrative interface

From both the places, users will be able to search using one or more DNA
or protein sequences. The homology search will be run on-the-fly, using
appropriate BLAST algorithm, against pre-computed genome-specific or
all-genome NR databases derived from reference genomes. The users will
be able to restrict the search to select genomes or genera. The results
will be displayed as table showing matching genomes or genomic features,
along with the summary of sequence alignment quality. In addition, the
narrative method will also show graphical alignment view. The users will
be able to select the search results and save them as genome or feature
set in the narrative.

We will also build new comparative analysis methods that support follow
up analysis of the feature sets. The enhanced Feature Set Viewer will
allow users to view the genomic features as table or profile of function
abundance or download features as tsv, excel, or FASTA files. A new MSA
and Tree method that will allow users construct multiple sequence
alignment and phylogenetic tree for a feature set using DNA or protein
sequences. The results will be displayed using an MSA + tree viewer and
also be available for download in standard file formats. A new Set
Comparison Method will allow users to select upto four genome sets or
feature sets, compare them, and view the results as Venn Diagram.

-   Team lead: Maulik

-   Team: Maulik, Fangfang, Harry (UI), Bob O.

### Extended description

The proposed Homology Search service is designed to allow a user to
rapidly query KBase public reference genomes and genomic features using
DNA or protein sequence, and find matching genomes, genes or proteins.
Similar to the keyword search functionality, this is one of the primary
entry points for the users who want to quickly find KBase reference
genomes and features matching their sequence of interest. From the
search results, they can go to the genome or feature landing pages to
get more information. Another objective of this service is to allow
users to explore potential function of a given gene or protein sequence,
which has influenced our selection of methods that we will develop to
support follow up analysis in KBase. The detailed description of various
components and methods proposed as part of homology search suite is as
follows.

1.  Pre-computed Homology Search Databases:

    To enable rapid homology search, we will pre-compute sequence search
    databases for the KBase reference genomes and deploy them via
    Homology Service. In the first phase, the homology search will be
    supported using BLAST. For every reference genome in KBase, we will
    construct genome-specific BLAST databases, containing genome
    sequences, gene sequences, and protein sequences. Taxon-specific
    BLAST databases, genus-level and higher, will be constructed by
    virtually aggregating corresponding genome-specific databases,
    without duplicating the data. In addition, we will also construct
    all-genome non-redundant (NR) gene and protein sequence databases by
    grouping features based on their MD5 checksum. For every feature
    group, only one representative feature will be included in the
    NR database. The FASTA definition line will summarize the function,
    as well as the number of identical features present in other
    reference genomes. We will develop scripts for constructing of the
    BLAST databases and updating them with every major data release.

2.  Homology Search Service:

    The homology service will provide programmatic access to various
    homology search algorithms, starting with the BLAST algorithms. The
    service will support search against pre-computed BLAST databases
    described in the previous section. The search API will allow users
    to select BLAST databases, restrict search to select taxon levels or
    genomes, select BLAST algorithm, and other parameters, such as
    number of hits and e-value cutoff. The service will return the
    search results as a pre-defined BLAST search result object, which
    will be built upon the object type defined by Genome Utilities
    campaign's BLAST
    method [*GenomeUtil.BlastOutput‑4.0*](https://narrative-ci.kbase.us/functional-site/#/spec/type/GenomeUtil.BlastOutput-4.0).

    In future, the homology service will be expanded to support
    ultrafast k-mer based homology search.

3.  Homology Search UI:

    The homology search UI will be accessible from the main KBase
    Reference Data Search page, allowing users to find genomes and genes
    of interest by using DNA or protein sequence, in addition to
    currently supported keyword search functionality. This search will
    be available to users without requiring login. When a user pastes a
    sequence in the search box, the sequence type will be automatically
    detected and appropriate default database and search algorithm will
    be selected, however, user will be free to overwrite the
    default selection. In addition to selecting pre-computed NR
    databases, user will also be able to specify a list of taxon or
    genomes to restrict the search scope. The search results will be
    presented as a table, showing matching genomes or genomic features,
    and related information such as genome name, gene function, and
    summary of alignment scores. The expanded view will show pairwise
    alignment between query and subject sequences. The results will be
    linked to corresponding data landing pages, where users can find
    detailed information. In addition, users will also be able to select
    one or more results and save them in narrative as genome or
    feature sets.

4.  Homology Search Narrative Method:

    The Homology Search Narrative Method will provide all the
    functionality that is described in the previous section for the
    Homology Search UI. In addition, it will also allow users to use
    previously created genome set as input and restrict the search to
    only those genomes. In addition to the tabular and pairwise
    alignment view, the narrative method will also provide graphical
    overview of the alignments, similar to that available at NCBI-BLAST.

    Previously, the Genome Utilities campaign developed a homology
    search tool that operates against user data, which is currently
    deployed
    into [*https://narrative-ci.kbase.us/*](https://narrative-ci.kbase.us/).
    We are proposing to ultimately subsume this tool into the new
    Homology Search method, which will support search against both
    public and user data. Given that our BLAST result object is build
    from the object type defined by Genome Utilities campaign's BLAST
    method, it will allow us to utilize some of the same viewers
    developed by the Genome Utilities campaign.

    In addition to viewing the homology search results, users will be
    able to select the matching genomes or genomic features and save
    them in narrative as genome set or feature set, respectively, which
    can then be used as input in the subsequent comparative analysis
    methods proposed below.

5.  Feature Set Viewer:

    KBase allows users to find genomic features of interest in multiple
    ways and save them as feature sets, so that they can be used in
    various follow up analysis methods. A feature set may contain genes
    with similar functions, genes with homologous sequences, or genes
    identified to be up or down regulated across one or more
    transcriptomics data sets.

    We will enhance the current narrative Feature Set Viewer to display
    more useful information in the tabular view, including genome name,
    feature id, function, gene name, and aliases. The users will be able
    to sort the table by any columns and filter it using keyword search.
    In addition, users will also be able to download feature sets in
    various different file formats, such as tsv, excel, and FASTA DNA or
    protein sequences.

6.  MSA and Tree Method:

    Multiple sequence alignment and gene trees are key tools used for
    comparative analysis of two or more homologous gene or
    protein sequences. They allow one to understand the evolutionary
    relationships among the homologs, identify conserved domains, and
    analyze single nucleotide polymorphisms. They can also help to
    detect and correct the translational start sites and frame-shift
    mutations or sequencing errors.

    The proposed MSA and Tree method will allow a user to start with a
    feature set, constructed using homology search or other methods
    available in KBase, and build multiple sequence alignment and
    phylogenetic tree by using corresponding DNA or protein sequences.
    In the first version, we propose to use Muscle for constructing MSA
    and FastTree for constructing phylogenetic tree from the alignment.
    Later, we can add other popular programs to the method, such as
    MAFFT and RaxML.

    The resulting multiple MSA and tree will be displayed side-by-side
    using an interactive JavaScript viewer. The viewer will allow users
    to highlight or collapse any branch of the tree. It will also show
    consensus alignment as Sequence Logo. The MSA and tree will also
    displayed separately in more traditional formats. In addition, the
    raw MSA and tree will also be available for download in standard
    formats, such as Clustalw and Newick, so that users can download and
    visualize them using other viewers available on the web.

7.  Set Comparison Method:

    We envision that KBase users will be constructing multiple genome
    and feature sets based on different selection or filtering criteria.
    For example, a user may create the following genome sets using the
    homology search method: a) genomes that contain gatA gene, b)
    genomes that contain gatB gene, and c) genomes that contain
    gatC gene. The user then wants to find which genomes contain all
    three genes, or genomes that contain any two of the genes, but not
    all three. The users with limited programing skills, it is often
    difficult to perform such analysis.

    The Set Comparison Method proposed here will allow users to select
    up to four genome or feature sets and compare them. The results will
    be displayed as Venn diagram, making it easier for users to find
    genome or features that are common to all sets, or present in some
    sets but not all. The users will be able to click on any parts of
    the Venn diagram, get the corresponding genome or feature list, and
    save it as a new set.

### Future Work:

1.  Homology search for private genomes:

    In future, homology search will allow users to search on public, as
    well as private user genomes. Users will be able use a genome set,
    which may contain public and private genomes of interest, and run
    homology search against these genomes. The homology search will
    detect the private genomes, build BLAST databases for them
    on-the-fly, and incorporate them into the search.

2.  Fast k-mer based similarity search:

    In future, homology search will support ultra-fast similarity search
    using k-mer technology. The k-mer based similarity search will
    return matches of a protein query sequence to a database of
    preloaded reference proteins.

### Timeline for feature release

**Sprint 1:** [January 2016]
-   Construct genome-specific BLAST databases for genomic sequences,
    genes and proteins
-   Design and implement Homology Search Service
-   Design and implement Homology Search UI v1

**Sprint 2:** [February 2016]
-   Construct all-genome NR gene and protein databases
-   Homology Search Service: Add support for NR databases and
    genome selection. Return BLAST Result object as output
-   Design and implement Homology Search Narrative Method v1

**Sprint 3:** [March 2016]
-   Deploy homology search databases and service in the ci environment
-   Refine homology search UI based on user feedback
-   Allow selection of search results and copy them to narrative

**Sprint 4:**
-   Add support for taxon selection in homology search service, search
    UI, and narrative method
-   Add support in the narrative method to select and save search results as genome or feature
    sets

**Sprint 5:**

-   Enhanced feature set viewer
    -   Table view: add more information. Support sorting and filtering
        by keyword
    -   Function abundance profile: A bar chart showing occurrences of
        gene functions in a feature set
    -   Download feature set data in various file formats, i.e. tsv,
        Excel, FASTA DNA and protein sequences

**Sprint 6:**
-   Design and implement MSA+Tree method, by wrapping Muscle and
    FastTree using SDK
-   Implement interactive MSA+tree viewer

**Sprint 7:**
-   Design and implement set Comparison method
-   Implement interactive Venn diagram viewer

### User stories

-   User Gyorgy comes to the KBase home page. He queries on the main
    search page for “thermotoga cellulose”. He selects one of the genes
    that comes up, opening up the gene page and copying the
    protein sequence. He then selects “sequence search” and pastes the
    protein sequence. He gets a list of homologous genes, which he
    copies to a narrative and then exports and downloads as a
    fasta file. He uses the homologs to attempt to find a version of a
    gene he can express in E. coli for protein crystallization.

-   User Chris runs a metabolic model and finds a dead end pathway
    consisting of ten steps, only one of which is present in his genome.
    He selects the gene in the model viewer and exports it to his
    narrative as a feature set, which he labels “orphan protein”. He
    then selects the homology search method, enters in his “orphan
    protein” object, hits submit. The results pop up. He looks in the
    functional distribution and finds that many of the homologs are
    annotated with a different role than the original orphan protein.
    Furthermore, that role is associated with a gapfilled reaction in
    his model. Chris then looks at the functional context analysis,
    which shows that his protein has a context that is much more
    consistent with this gapfilled function than with the
    original function. Chris reannotates the protein and rebuilds
    the model.

### Narrative mockups

The output from each of the methods described above is presented in the
mock graphics below.

**Homology Search UI:**

<image src="https://github.com/kbase/homology_service/blob/master/docs/images/Homology_search_UI.png" width="600px"/>

**Homology Search Results:**

<image src="https://github.com/kbase/homology_service/blob/master/docs/images/Homology_search_results.png" width="600px"/>

**Feature Viewer:**

<image src="https://github.com/kbase/homology_service/blob/master/docs/images/Function_profile.png" width="400px"/>

**MSA and Tree Viewer:**

<image src="https://github.com/kbase/homology_service/blob/master/docs/images/MSA_and_tree_viewer.png" width="800px"/>

**Set Comparison Viewer:**

<image src="https://github.com/kbase/homology_service/blob/master/docs/images/Set_comparison_viewer.png" width="400px"/>
