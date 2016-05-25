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

To simplify this, the developer needs: 

* A lightweight, easy to understand process for generating files from KBase Objects. 
* This method needs to be centrally managed. 
* Hide details of KBase typing system and architecture. 
* Perform all error handling and manage warnings. 
* For saving KBase typed objects, an easy process for generating metadata from a parent object will also be needed.
* The file generation should run on the already provisioned compute node.
* Updates to the file generation code (service/method/script/etc) should not require the SDK module to be rebuilt.
* The process for adding a new convert should be easy and available to 3rd party devs.
* Developers should be able to easily browse all available object to file converters (like the AppCatalog)
* Adding a new converter should not require a redeploy of the KBase platform.


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

