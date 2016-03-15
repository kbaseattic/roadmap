## Data to File Services

### Summary
A significant use of the KBase SDK is for wrapping existing command line tools. These tools rely on (relatively standard) file formats for input and output. For a developer, a great deal of specialized knowledge about the KBase types, typing system and underlying data stores is necessary to generate files from KBase types. This proposal aims to simplify the process of generating files from KBase types and saving KBase types from files.

### Story/Description
Currently, a developer needs to know too much detail about the KBase data object, the typing system and the data stores. For example, let’s consider reads. To generate a fastq file from a reads typed object, you need to understand: 

* The reads types defined in both the KBaseAssembly and KBaseFile namespaces. 
* How to pull objects from the KBase Workspace. 
* The nested relationships defined by the types.
* The KBase Handle service.
* The KBase Shock service.
* How to pull files from the KBase SHOCK data store.
* How to authenticate independently across the multiple data services involved.
* Indirect indication that paired ends reads are interleaved.
* Indirect indication that reads are compressed.
* Most importantly, the user has to understand all the possible error states of the Workspace, Handle and SHOCK services.

This process takes ~200 lines of code to implement in current SDK methods. And any bug fix or additional error checking would have to be independently done in each method. 

To simplify this, the developer needs access to a lightweight, easy to understand process for generating files. This method needs to be centrally managed, hide details of KBase typing system and architecture, and perform all error handling and manage warnings. For saving KBase typed objects, an easy process for generating metadata from a parent object will also be needed. 

Because the SDK methods will be running on already provisioned compute, it is desirable to use the local compute resources as much as possible. 

It should be easy to add a new converter, without requiring a redeploy of the KBase platform.

Developers should be able to easily browse all the available object to file converters.

### User Stories
As a developer, I would like to be able to easily generate a file from a KBase typed object to use as input to a command line program.

As a developer, I would like access to tools/methods to convert between common file formats.

As a developer, I would like to easily add my own converter. 

### Narrative Mockup
N/A

### Timeline
To be determined in consultation with the Production Leads.

### Test Plan


### Citations
N/A

