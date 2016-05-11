## Bulk Upload Download Product Description:

### Summary
This will enable upload and download operations on more than one object at a time.

### Story/Description
We are proposing the following user experience to support bulk upload and download. 

#### Bulk upload:
1. Users load their files in an authenticated FTP staging area. We would not provide an explicit UI for this, as numerous UI clients already exist for performing this kind of transfer, including the web browser itself.

2. Once files are loaded, users transition selected sets of files from the FTP staging area to one or more narratives accessable to the user (or new narratives). For this, we would offer a UI, linked off of the narrative hamburger menu or dashboard. This UI would enable the user to select any number of files of the same type for transfer and specify the KBase data type that should be created. Then, users will be presented with a spreadsheet-like form to enter any parameters or metadata needed to convert the files to specified KBase types. This form would include practical information like which narratives the user wants to transfer to (they could put different objects in different narratives), as well as needed parameters for the conversion (biomass reaction and genome for SBML files). This form could also ultimately support metadata (e.g. where were these imported genomes isolated from?). This form would support some type of "auto-fill" capabilities like those in excel, to reduce the tedium of filling out the form for large numbers of objects.

3. Once the transfer parameters form is complete, users would click on a "submit" button. This would trigger the creation of a data transfer job and also return the user to the file selection page. On  the file selection page, the files the user selected for previous transfers would be marked with a status indicating the transfer was in progress and offering the chance to cancel the transfer.

4. We could offer a simplified version of this interface as a method in the narrative itself. This interface would be simplified, because it would only permit the user to transfer files to the narrative that they run the method in.

#### Bulk download
For bulk download, we have multiple options we can explore. Arguably, both are valuable and should probably be implemented at some point.

#### Option 1 - offer all narrative data seamlessly via FTP:
Here we propose to offer an FTP address for each user (e.g. ftp://kbase.us/<username>/), and at this address, the user would be presented with a virtual file space laying out all their data organized by type or by narrative. See these examples:

- Go to ftp://kbase.us/<username>/narratives/, and see a list of narratives
- Go to ftp://kbase.us/<username>/narratives/Test narrative/, and see the names of all objects in narrative named "Test narrative"
- Go to ftp://kbase.us/<username>/narratives/Test narrative/SB2B genome/, and see a list of all download formats for a genome
- Go to ftp://kbase.us/<username>/types/, as see all data types the user has in the system
- Go to ftp://kbase.us/<username>/types/KBaseGenome/, and see all narratives accessible by the user containing a genome
- Go to ftp://kbase.us/<username>/types/KBaseGenome/Test narrative/, and see all narratives accessible by the user containing a genome
- Go to ftp://kbase.us/reference_data/, and see all data types where KBase has reference data
- Go to ftp://kbase.us/public/, and see data from public narratives
- Go to ftp://kbase.us/featured/, and see data from features narratives

Users would be able to use standard FTP tools to select any files for download that they want. File transfer requests would kick off the conversion of the object to files on the fly.

#### Option 2 - bulk download from within a narrative:
Here, we would offer a new "Bulk download" method in the narrative itself, encoded in SDK. Essentially, this method would first ask users to select a data type. Then it would present users with a list of available files types for that data type (e.g. JSON, SBML, and TSV for a model). Then users would be able to either select objects one at a time using the current dropdown interface, or click a checkbox indicating that all objects of the specified type should be downloaded. When users click the "run" button, this triggers an SDK job that downloads and converts all the objects, loads everything into a zip archive, pushes the zip archive to shock, and places a download link in narrative. We would need manage ACLs on the download link somehow, probably handle service.

#### Bulk download:
 for user files, where every user has their own FTP "inbox". They can upload files into this "inbox", but if they do not progress to moving the files into the narrative as KBase objects within a specified time frame, the files could be automatically deleted. 

### User stories

- User 1 would like to upload 100 raw read files, provide distinct names, link to conditions, and ultimately prep for the RNAseq pipeline.
- User 2 would like to download all publically available Brucella genomes.
- User 3 would like to upload a directory containing 10 FBA models.

### Narrative Mockup

### Timeline

#### Sprint 1

1. Create simple FTP upload staging zone
2. Create mockups for upload UI
3. Develop plan to convert uploader to SDK methods

#### Sprint 2
1. Convert one upload to SDK method (likely genome) 
2. Create simplified method for translating staged files into narrative objects
3. Implement service backend for FTP staging area
4. Refine FTP staging zone

#### Sprint 3 
1. Complete method for translating staged files into narrative objects
2. Prototype UI for bulk translation of staged FTP files into narrative objects
3. Complete FTP staging zone
4. Convert additional existing transform methods to SDK methods
5. Initial implementation of FTP download of one type

#### Sprint 4
1. Refine UI for bulk translation of staged FTP files into narrative objects
2. Update upload method in narrative replacing simplified place-holder with real method
3. Complete FTP download paradigm for narrative objects

#### Sprint 5
1. Perform user testing
2. Create / Update user documentation

### Test plan
1. Test all functionality as each feature is completed in each narrative.

### Citations
N/A


