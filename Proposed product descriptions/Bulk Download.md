

# Bulk Download Product Description

## Summary
This will enable bulk download operations.  

## Story / Description

The ability to download objects of a particular user-defined class has been requested from multiple users.  We anticipate an increasing need for this functionality as the number of returning users to the system grows.  Returning users will have an ever growing amount of derived data in the system, and downloading this data via the current single object methods is a tedious process.  Additionally, we have recieved requests from users who would like to download some or all of the reference data in the system.  By enabling this we also make it easier for other systems to integrate with KBase. 

This will extend the bulk upload user interface created during the Bulk Upload campaign to provide download functionality.  A link will be created or updated in the data panel to connect this feature to the existing data import/export functions.  That link will take users to a bulk download operation page. That page will provide multiple object selection, with the ability to search minimally by workspace and type.  Selection boxes will be provided next to each object, along with a select all function.  Once the user has completed their selections, an export button will submit a series of jobs to the backend. The backend job will instantiate SDK methods from the function catalog to export the data to the users DTN staging area.  Once the export job is completed, the user will be notified on the bulk upload/download status page.  A link from the notification will bring the user to a preconfigured globusonline download page, where they can select the target endpoint and complete the bulk transfer out of the system.

Here are some relevant JIRA tickets from external users requesting this functionality:  
https://atlassian.kbase.us/browse/KBASE-620  
https://atlassian.kbase.us/browse/KBASE-477  
https://atlassian.kbase.us/browse/KBASE-3427  
https://atlassian.kbase.us/browse/KBASE-1732  

## User Stories
- User A would like to download all of the reference genomes in KBase
- User B would like to download all of the genomes available in a specific workspace
- User C would like to download all of the paired end reads in a specific workspace

## Timeline
+ Sprint 1: Mock up UI modifications.  Add a dev sdk method for downloading read data.  
+ Sprint 2: Begin UI implementation. Add links to narrative data panel. Integrate download UI page with type catalog.
+ Sprint 3: Complete UI page.  Complete end to end download method, and execution path from data store to staging area.
+ Sprint 4: Complete integration - link out/in to globus download page.
+ Sprint 5: User testing, corrections from results of user testing.

## Test Plan
We will test the bulk download methods internally during the maintenance weeks.  User testing plans, scripts, and scheduling will occur during Sprint 4, and the actual user test session will occur during the first week of Sprint 5.


