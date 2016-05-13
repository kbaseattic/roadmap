# Rapid data access for large Genomes

## Summary

There are performance issues with how data is organized and stored in our system that have not been addressed and likely will not be addressed before the end of Q2.  Instead of attempting to address performance issues for every type, it makes sense to focus efforts on the Genome types first, to determine what the specific solutions would be for those types.

Data API methods would provide faster access to all Genome data and would have a recipe for how to store new types and modify existing ones for performance.  This would speed up Landing Pages, Search indexing, file creation from genome data including bulk download, etc.

## Description

Data in KBAse is currently organized into either only JSON documents, or some combination of JSON documents and Blob data containing files.

The workspace data store keeps KBase objects (represented as JSON documents) in a Mongo DB if the size of the document is less than 16MB.  If the document data is larger, the data is actually stored as a Blob in the SHOCK data store.  The vast majority of Eukaryotic genome data will fall into the latter category.  So to fetch an object for a Eukaryotic genome, a workspace client requests the object, the workspace service then checks to see if it has the data, then makes a call to SHOCK to request the JSON as a Blob.  The Blob comes back and then is parsed by the workspace service, and if the data is larger than memory the JSON is first written to disk and then read back to construct the message body for the response to the workspace client.  From the Data API, at least 95% of time is spent just fetching object data from the workspace, regardless of any subsetting requets to the workspace.  So minimizing the time spent transferring data is the most effective optimization we can make from Data API.  Even if requesting a subset of information from the object, the entire JSON must be extracted from SHOCK, then parsed and subset at the workspace service level, then passed back to the client.  What we found working with Data API was that over and over this was the most time consuming step, and so the only optimization that could be done if the system design was fixed, which it effectively was, was to reduce by any means the size of the JSON documents.

The Assembly type was designed to keep the FASTA data in a Blob in SHOCK, and then populate the JSON document with high level summary information and an index of the file that would provide a way to pull out individual sequences as needed.  In hindsight we should have followed this same approach for the GenomeAnnotation type.  Instead, we split the JSON data into more documents, thinking that each document would be smaller.  However, this approach simply exacerbated the above problem by requiring even more two hop fetches on JSON data, with some data still creating fairly large documents for each feature type.  So we could store larger data, which was an improvement, but we could not store just any large data because of workspace object size limits (which are not the core problem here), so we had to build in ways to drop data if it exceeded the object size limits until we could fix the underlying storage problem, which would also address performance issues, particularly when filtering data.

The work involved here would be refactoring the data storage scheme for GenomeAnnotation data to store as much data as possible in the form of Blobs, while keeping an absolute minimal amount of information in JSON documents to minimize the performance issues we encountered.  This is our only path forward in the short term given the current fixed system design.  Data API methods would optimize the filtering and extraction of the Blob and JSON data as much as possible, supporting all parts of the system that rely on fast access to genome data, including but not limited to Landing Pages, Search indexing, converters to files.

## Risks

Blob API supports this work because we can more efficiently store and access the genome data using blobs and lookup information for those blobs.  This means Blob API should be completed first.

Refactoring the storage of the new Genome types would severely impact any code that did not use Data API for data access.
