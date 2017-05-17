# Blob Data API

## Summary

The Blob Data API would provide the following capabilities for developers, 1) listing Blob data connected to a KBase object, 2) creating a Blob from bytes of data, 3) attaching a Blob to a KBase object with metadata, 4) removing an attachment of a Blob from a KBase object, 5) retrieving Blob data, 6) sharing Blob data.

Users would experience improved performance in the system for components that currently use Blob data and have migrated to use the Blob API.  Users would have a consistent experience sharing any KBase objects that had Blob data associated with them.  Provenance data would be recorded for every Blob in the system, increasing the available insight into how data was created or modified.  Developers would have a better experience working with Blob data in KBase through improved system performance and reduced complexity.

## Description

In our current system, there are two possible ways to store data permanently, as a JSON document, or simply as bytes of data.  KBase objects have a 1GB size limit per JSON document, with a 1:1 mapping between KBase type and JSON document.  Storing large data via JSON documents requires the definition of multiple types and then potentially complex mappings between those types.

(Blob) https://en.wikipedia.org/wiki/Binary_large_object

A blob is defined here as bytes of data with a small amount of user defined metadata, including required provenance and a MIME type for the data.  Blob data must be attached to a KBase object to be permanently accessible, and can be part of the primary data representing a type, or can be derived or ancillary data that should be saved for reference or for further computation. 

KBase does not impose a limit on the size of a Blob, leaving a simpler path for storing large data.  There are also performance advantages to storing large data in other formats besides JSON, both in storage efficiency and parsing or processing efficiency.  So the performance of large data is largely dependent on Blobs in KBase.  Large data is also vital to many key biological workflows and analyses, making the performance and ease of use of that data in KBase important.

References to Blob data are currently explicitly declared in each type, with each type storing the references in different places with different field names, with the references being potentially optional.  This requires developers to understand how every type chooses to store Blob references if they need the Blob data.  It also means that if an additional Blob should be added to an object, one that was not already defined in the type specification, a developer who is not the owner of the type may be forced to create a new type simply to store the Blob.  One potential way to address this would be to require that every type include a standard structure for storage of Blob references, although there is currently absolutely no requirement on the structure for any KBase type.  Another way to address this would be to store the Blob references outside of the KBase object, which could be another KBase type storing the references, or (further down the road) another data store to contain those references independent of any KBase objects.

There is also not currently a consistent sharing model between KBase objects and KBase blob data.  KBase objects that are shared do not propagate the access permissions to connected Blob data in all cases.  Part of this is due to inconsistency in how KBase Blob reference types are used (since we have two), but another part is that there is an inconsistency between how our KBase object store handles permissions and how our KBase Blob store handles permissions.

This product would provide a simple API for Blob data, making that data easier to work with as a developer, would provide improved performance, and would enable a consistent sharing model between KBase objects and KBase Blob data.

## User Stories

As a developer, I would like to make an API call to see a listing of all the Blob data associated with a KBase object, with information about each Blob.

As a developer, I would like to easily determine through an API call if a KBase object has a particular piece of Blob data.

As a developer, I would like to easily create Blob data and dynamically associate any Blob with any KBase object using API calls.

As a developer, I would like to easily remove a Blob data association with a KBase object using an API call.

As a developer, I would like to be able to retrieve Blob data using an API call.

As a developer, I would like to be able to retrieve subsets of Blob data using API calls.

As a user, I would like to share my KBase objects and automatically share all underlying data with the same access permissions.  

## Risks

The ability to more easily produce and consume Blob data in the system could increase stress on our current Blob data store and increase the need to replace with an enterprise grade store.

To reap the benefits of the Blob Data API, all code in the system that interacts with Blob data would need to be modified to instead use the Blob API.  For instance, data sharing would need to go through the Data API to maintain consistency of permissions.

With increased flexibility to associate any Blob data with any KBase object, it emphasizes the importance of code review and rigorous testing to prevent misuse or abuse of the system.
