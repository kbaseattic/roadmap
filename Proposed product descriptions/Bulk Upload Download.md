## Bulk Upload Product Description:

### Summary
This will enable upload operations on more than one object at a time.

### Story/Description
We are proposing the following user experience to support bulk upload. 

#### Bulk upload:
1. Users load their files in an authenticated FTP staging area. We would not provide an explicit UI for this, as numerous UI clients already exist for performing this kind of transfer, including the web browser itself.

2. Once files are loaded, users transition selected sets of files from the FTP staging area to one or more narratives accessable to the user (or new narratives). For this, we would offer a UI, linked off of the narrative hamburger menu or dashboard. This UI would enable the user to select any number of files of the same type for transfer and specify the KBase data type that should be created. Then, users will be presented with a spreadsheet-like form to enter any parameters or metadata needed to convert the files to specified KBase types. This form would include practical information like which narratives the user wants to transfer to (they could put different objects in different narratives), as well as needed parameters for the conversion (biomass reaction and genome for SBML files). This form could also ultimately support metadata (e.g. where were these imported genomes isolated from?). This form would support some type of "auto-fill" capabilities like those in excel, to reduce the tedium of filling out the form for large numbers of objects.

3. Once the transfer parameters form is complete, users would click on a "submit" button. This would trigger the creation of a data transfer job and also return the user to the file selection page. On  the file selection page, the files the user selected for previous transfers would be marked with a status indicating the transfer was in progress and offering the chance to cancel the transfer.

4. We could offer a simplified version of this interface as a method in the narrative itself. This interface would be simplified, because it would only permit the user to transfer files to the narrative that they run the method in.


### User stories

- User 1 would like to upload 100 raw read files, provide distinct names, link to conditions, and ultimately prep for the RNAseq pipeline.
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

#### Sprint 4
1. Refine UI for bulk translation of staged FTP files into narrative objects
2. Update upload method in narrative replacing simplified place-holder with real method

#### Sprint 5
1. Perform user testing
2. Create / Update user documentation

### Test plan
1. Test all functionality as each feature is completed in each narrative.

### Citations
N/A


