# Sequence Types

## Summary

This effort would involve the creation of new types for any sequence data or grouping of sequence data that are needed but not currently captured in our system.  We would standardize existing sequence types for Reads, Assembly, GenomeAnnotation, distinguish between DNA, RNA, and AA sequences, and provide common Data APIs for Sequence types.  This work would provide improved upload and download for sequence data through better quality types and objects, improved or actual Landing Pages for sequence types, Narrative viewers where missing, and mechanisms for data manipulation of sequences.

## Description

KBase currently defines a number of types that contain sequence data, however there is little to no commonality between these types other than that they store sequence in a string.  We do not capture the sequence type or alphabet of the sequence in these types.  By default we should attempt to apply an IUPAC alphabet to the sequence if no alphabet is given.  We should appropriately identify on upload if data is DNA, RNA, or AA sequence and tag it appropriately.  We need commonly defined sequence container types that can be reused as building blocks for more complex types.  We also need types that can be used for aggregating sequence information and grouping them.

For consistency and quality purposes, we would create a single common definition for what information should be captured for any sequence data in our system, and then universally use that definition unless there is a very good reason to make an exception.  Additionally, to simplify working with different types that contain sequence, we would develop a common API for working with sequences and retrieving them.  This way once you learn how to use the API for one sequence type, you will not need to learn it again for another.

For GenomeAnnotation and Assembly types, we can also capture the genetic code information and include that from any SequenceSet created from those types.

We would evaluate compression schemes for sequence data to determine if there is an acceptable compression that improves transfer performance while maintaining easy indexing.

Work on improving sequence data interaction and visualization would be coordinated in conjunction with the UI team.

## Risks

This relies on the Blob Data API work existing.  Without Blob Data API, we would have to deal with storing sequence data via Blobs here and then again for any new types in the future that depend on Blob data.

## User Stories
* A user is running on KBase objects that contain sequence data. Transparently to this user, the underlying services access the sequence data through the Sequence API, which rests on top of the Blob API, and transparently attempts to attain maximum efficiency using compression, caching, and indexing of the underlying data. The user experiences this as higher performance for their analysis.
* A user views an Assembly in the narrative or landing pages. The sequence data part of this assembly is rendered using widgets that are shared across all sequence types.  Some of the details of a given visualization will be specific to the sequence sub-type, but the majority of the code will be shared. Improvements and additions to these viewers will affect (and improve) multiple sequence sub-types.
* An external developer wishes to create a new data type, custom to their pipeline, that includes selected contigs (passing some filter) from an Assembly. Rather than store these as a custom string, the user defines these contigs as a SequenceSet and, from there is able to use the Sequence API to create, validate, and access this data.
* A power-user has some code written in Python using the scikit-bio interface. He wants to use this same code in code cells in the Narrative. He uses the Data API to pull selected data from KBase objects and then can use a scikit-bio compatibility layer to the Sequence API to integrate his existing code with minimal changes.

## Citations

Reference information

http://www.ncbi.nlm.nih.gov/IEB/ToolBox/SDKDOCS/BIOSEQ.HTML
https://en.wikipedia.org/wiki/International_Union_of_Pure_and_Applied_Chemistry#Amino_acid_and_nucleotide_base_codes
http://biopython.org/wiki/SeqRecord
http://scikit-bio.org/docs/0.2.0/sequence.html
