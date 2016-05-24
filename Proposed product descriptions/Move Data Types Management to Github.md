## Move Data Types Management to GitHub

### Summary

Move the management of data types from the current workspace admin model to using standard Github practices.

### Story/Description

Types are currently managed by the workspace service through
a set of KIDL defined interfaces.  This has worked well but
a number of weaknesses have become evident over time.  One
is that the process for adding types can be difficult to
comprehend.  Secondly, it is difficult to get a holistic view
of all the types in the system.  Third, once someone owns a
namespace, they have unfettered control to add types without
any review.  Fourth, moving a defined set of types from one
environment is extremely difficult and the types can easily
move out of sync.  This makes it hard to maintain a
consistent set of types between CI, next, production and
appdev.

#### Approach

The proposed solution is to migrate managing the types to a public github repo.  Adding or changing types would be managed through the typical "pull request" and merge process of github.  This would allow for more review.  A group of KBase reviewers would be responsbile for reviewing the addition of types and could use the comment system to suggest changes or reject a PR if it is poorly defined or closely duplicates an existing type.

The current methods for type management in the workspace would be removed.  The types would be pulled from a configurable GitHub repo.  The workspace would be modified to either a) directly pull the types from the repo or b) talk to a new service that would pull the types from the repo.

The logic for how types are versioned would remain unchanged but the mechanism would need to be changed.  It is important the current checks for type versioning are enforced.  The workspace could continue to do a final check, but a post-commit check could be used to assign the version using the existing logic or validate the proposed version.  In the later scenario, the type proposer would use a command-line tool to generate the correct version number.

Different type versions could be tracked via the history or as separate files.  This means all versions of a type would be visible doing an ls.  The implementation team should decide which approach is most appropriate.

#### Documentation

Existing documentation would need to be updated to reflect the revised process.

### User stories

No changes should be evident to a bench biologist.

A SDK developer can fork the github types repo and create a new type.  They can add and commit the new type, push it to their private repo and issue a pull request to the upstream types repo.

A KBase Data Types manager can review PRs for new types and comment through the Github comment system.  Data type managers can request expert review for data types they lack expertise with.

A PR can be merged and the new data type should be detected by any KBase deployment with 5 minutes and be available for use.

A travis CI check or other post-commit check would validate any new types to make sure they are valid.  The check would either automatically assign the appropriate version number or validate the proposed version number.

Type Versioning should remain unchanged from the current model once the type is added to the system.

### Narrative Mockup

N/A

### Timeline

This work would be completed in 1-2 two sprints.


### Test plan

Need to flesh this out.

### Citations

N/A
