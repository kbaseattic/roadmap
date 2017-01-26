### Summary

This proposed work will automatically create a set of citations in a user's Narrative, based on which Methods are run in that Narrative.

### Description

Each KBase Narrative is based on running a series of scientific Methods, with the goal of telling a coherent scientific story that can, eventually, become a formally published article. Each analytical method used in the Narrative is the culmination of work by several researchers, and that work should be cited in the Narrative. Most scientific publications contain a section devoted to citations, which can produce some tedious work for the researcher. However, since Narrative methods already reference their appropriate citations, these should be automatically introduced into a References or Citations section.

This proposed work would automatically produce and update such a reference section. Each Method run to produce data in the Narrative would add to the references, and would contain a link to view them in place. References should also be introduceable by the user adding text to Markdown cells.

The references section would be a collapsible, optionally viewable portion of the Narrative. This section should be editable to introduce user-chosen references that can be added inline in Markdown cells (though Method-linked refs should not be editable).

References should follow the XXX format, appearing in the order in which they are referenced in the Narrative.

### User Stories

1. User A starts a Method that produces data. This also adds one or more methods in the order set by the order in which that cell is included.

2. User B runs several methods, adding multiple references, then changes the order in which those cells appear. The references should then change their order to match.

3. User C runs a few methods, producing some references, then wants to add a reference to a Markdown cell. This Markdown reference should appear in the proper order in the list of references.

4. User D runs a method, producing some data and references. She then removes that method from the Narrative.

### Narrative Mockup

Design mocks should be produced as part of the work.

### Timeline

One-two sprints
  1. Design and mockup the area that would show the references, link them to the proper cells, and serialize them in the Narrative typed object.
  2. Test this design mockup with KBase internal scientists.
  3. (Optionally) iterate on design.
  4. Implement finalized design.
  5. Test results.

### Test Plan

This will be in two forms - user testing with a prototype, asking for simple tasks to be performed (Find the list of references, add one), and unit and integration testing of the code changes.

### Citations

N/A - this is an internal change with code we're writing.