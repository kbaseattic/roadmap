# Rapid data access for large Genomes

## Summary

There are performance issues with how data is organized and stored in our system that have not been addressed and likely will not be addressed before the end of Q2.  Instead of attempting to address performance issues for every type, it makes sense to focus efforts on the Genome types first, to determine what the specific solutions would be for those types.  At the end of Q3, Data API methods would provide faster access to all Genome data and would have a recipe for how to store new types and modify existing ones for performance.  This would speed up Landing Pages, Search indexing, file creation from genome data including bulk download, etc.

Blob API supports this work because we can more efficiently store and access the genome data using blobs and lookup information for those blobs.
