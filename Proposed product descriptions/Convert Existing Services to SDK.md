## Convert Existing Science Services to SDK

Formal Sprints for Current Tool Optimization - Port Annotation to SDK	Shane

### Summary

Their are multiple reasons to migrate our existing science services to the SDK framework.
First, the SDK simplifies updating and maintaining services, so bug fixes can be more quickly
deployed, tested and released.  Secondly, the SDK execution engine provides better tracking
and error reporting.  Thirdly, having all services in the SDK demonstrates to the community
that all services run in a consistent manner (i.e. KBase developed services don't receive some
special status).

### Story/Description

Methods that need to be migrated and approximate difficulty
- Genome Annotation - difficult but partially complete
- Assembly (still running through the ARAST service)
- Trees (status)
- CoExpression (complete?)
- GenomeComparison
- KBaseFBAModeling (Complete)
- KBaseFeatureValues (easy)
- KBaseGeneFamilies (easy)
- KBaseTrees (Complete?)

### User Stores

The user stories are fairly intuitive.  Users should be able to run all existing services with
little to no change in behavior.  Method parameters and options should be identical to the legacy
version unless it is decided that improvements should be made during the migration process.

### Testing Plan

Legacy methods will remain visible on the test system so that the behavior of the legacy method and
migrated method can be easily compared.

Independent internal testers will execute the migrated methods following any existing tutorials or documentation
to ensure consistency.

### Narrative Mockup

The existing methods will be used so the narrative experience will be unchanged.

### Timeline

This can be completed in a single sprint.  It should be done early so we can simplify the overall architecture and gain consistency.

### Citations

N/A
