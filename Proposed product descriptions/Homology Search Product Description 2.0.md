Homology Search 2.0 Product Description
===================================

### Summary

Previously, we had a series of sprints dedicated to homology search, which resulted in the development of a new homology search service, and the addition of a new homology search service for querying reference genomes for homologous genes.

This previous work resulted in only minimal functionality within the narrative, which requires expansion before it can be effectively deployed. In this PD, we are proposing to complete a sufficient ecology of homology tools within narrative to permit the deploy of this functionality and enable a rich experience of homology analysis within the narrative. A major side benefit/goal of this PD is to make the FeatureSet a first class object in Narrative.

### Extended description

This PD is about developing a sufficient ecology of homology tools within narrative.

1.  Refine or introduce new FeatureSet type that supports stand-alone genes

    KBase allows users to find genomic features of interest in multiple
    ways and save them as feature sets, so that they can be used in
    various follow up analysis methods. A feature set may contain genes
    with similar functions, genes with homologous sequences, or genes
    identified to be up or down regulated across one or more
    transcriptomics data sets.
    
    Currently, the FeatureSet object in KBase only supports features that are included in 
    Genome objects. We propose to work with the data team to revise the existing
    FeatureSet, or introduce a new object, that will permit the representation of 
    standalone genes. This includes spec-ing the type, creating uploaders, creating
    downloaders, and creating/updating viewers. Downloaders will support a variety of
    formats, including tsv, excel, and FASTA DNA or protein sequences. The viewer will
    display more useful information in the tabular view, including genome name,
    feature id, function, gene name, and aliases. The users will be able to sort the table
    by any columns and filter it using keyword search. The viewer will also show a bar 
    chart profile of the functions contained in the feature set.
    
    We will then adjust the homology search interface, which currently only moves genome
    objects associated with homology hits into narratives, to create FeatureSet objects of
    homology hits in narratives.
    
2.  Refine homology search narrative method:

	We are proposing to complete the release of our homology search narrative method,
	which will enable users to query the homology search service with either a feature
	set, or a pasted string of sequence data within the narrative. We will re-use the
	output types and viewers from the Genome Utilities campaign's BLAST method. In
	addition to the tabular and pairwise alignment view, the narrative method will also
	provide graphical overview of the alignments, similar to that available at NCBI-BLAST. 
	Users will be able to select the matching features from homology search results and 
	save them in narrative as a FeatureSet for further analysis. 
	
3.  Tool for homology-based annotation reassignment:

	This tool will take the output of a homology search as input, as well as a genome 
	object. The tool will then look at all features in the genome that are queried in the
	homology search output, and it will look at the list of unique functions associated 
	with the hits for each query feature. A compare-regions type view will show the 
	context of each query gene and each homology hit. The user will then be given the 
	option of re-annotating each of the genes with one of the functions assigned to one of 
	the homology hits. The results will be saved as a new genome object.

4.  MSA and Tree Method (OPTIONAL - ONLY IF THERE IS TIME):

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

5.  Set Comparison Method (OPTIONAL - ONLY IF THERE IS TIME)

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

### Timeline for feature release

**Sprint 1:**
-	Refine spec for FeatureSet object
-   Refine FeatureSet upload and download tools
-   Enhanced feature set viewer
-   Add narrative method for homology search
-   Document and test new features

**Sprint 2:**
-   Design and implement MSA+Tree method, by wrapping Muscle and
    FastTree using SDK
-   Implement interactive MSA+tree viewer
-   Design and implement annotation reassignment tool
-   Refine tools and documentation form sprint 1 based on feedback
-   Document and test new features in sprint 2

### User stories

-   User Chris runs a metabolic model and finds a dead end pathway
    consisting of ten steps, only one of which is present in his genome.
    He selects the gene in the model viewer and exports it to his
    narrative as a feature set, which he labels “orphan protein”. He
    then selects the homology search method, enters in his “orphan
    protein” object, hits submit. The results pop up. He loads the results into the 
    annotation reassignment tool, altering annotations in his genome to fill the gap in 
    his pathway. He rebuilds the model, which no longer contains the gap.

### Narrative mockups

The output from each of the methods described above is presented in the
mock graphics below.

**Feature Viewer:**

<image src="https://github.com/kbase/homology_service/blob/master/docs/images/Function_profile.png" width="400px"/>

**MSA and Tree Viewer:**
