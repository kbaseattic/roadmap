# Execution Engine HPC Integration

## Summary
This will extend our backend execution engine with additional capabilities.

## Story/Description

This will address the log jamming and lack of scalability in the execution engine and the need to enable HPC job execution to allow us to exploit our HPC compute facilities.

## User stories
User 1 would like to run 100 metagenome assemblies.  
User 2 would like to run an nr search across 2000 uploaded contigs.  
User 3 would like to run 2000 FBA models.  

## Narrative Mockup
N/A

## Timeline
#### Sprint 1 
1. Evaluate options for execution engine.  Begin implementation plan.

#### Sprint 2
1. Complete implementation plan
2. First cut implementation of the EE

#### Sprint 3 
1. Deploy EE on test environment
2. Deploy EE on test HPC environment (beagle?) 

#### Sprint 4
1. Port one workflow method to HPC backend - current target is tuxedo
2. Correct any problems identified with method execution

#### Sprint 5
1. Performance tuning
2. Update developer documentation

## Test plan
1. Test each user story after the sprint that implements the functionality
2. Scalability testing will occur during sprint 3/4

## Citations
N/A
