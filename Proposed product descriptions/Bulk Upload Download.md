## Bulk Upload Download Product Description:


### Summary
This will enable upload and download operations on more than one object at a time.

### Story/Description
We have recieved many requests for bulk object upload/download operations.  This should be done now as bulk file operations are widely available to users of other web services.  

### User stories

- User 1 would like to upload 100 raw read files.
- User 2 would like to download all publically available Brucella genomes.
- User 3 would like to upload a directory containing 10 FBA models.

### Narrative Mockup

### Timeline

#### Sprint 1 
1. Enable upload/download to run as SDK methods using the same infrastructure as the other narrative methods.
2. Increase backend capacity for upload/download jobs. 
3. Prepare dropbox-like target using GlobusOnline

#### Sprint 2
1. Design and implement web interface for dropbox-like target
2. Enable batch processing triggered by uploads or schedule for backend

#### Sprint 3 
1. Design bulk interface for downloads

#### Sprint 4
1. Implement bulk interface for downloads

#### Sprint 5
1. Performance tuning

### Test plan
1. Test each user story after the sprint that implements the functionality

### Citations
N/A


