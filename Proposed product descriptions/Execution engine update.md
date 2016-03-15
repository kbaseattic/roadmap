## Execution engine update


### Summary
This will implement a new backend execution engine with additional capabilities.

### Story/Description

The log jamming and poor communication in the execution engine (partly addressed by SDK and your error reporting) and the need to enable HPC job execution to allow us to exploit our unique compute facilities and make required connections to JGI, etc requires attention. We need a better engine, and API for manipulation, and an HPC solution.

### User stories
User 1 would like to run 100 metagenome assemblies.
User 2 would like to run an nr search across 2000 uploaded contigs.
User 3 would like to run 2000 FBA models.

### Narrative Mockup

### Timeline
#### Sprint 1 
1. Evaluate options for execution engine
#### Sprint 2
1. Design the EE
2. First cut implementation of the EE
#### Sprint 3 
1. Deploy EE on test environment (CI?) 
2. Deploy EE on test HPC environment (beagle?) 
#### Sprint 4
1. Iterate through existing methods
2. Correct any problems identified with existing method execution
#### Sprint 5
1. Performance tuning

### Test plan
1. Test each user story after the sprint that implements the functionality
2. Scalability testing will occur during sprint 3/4

### Citations
N/A


