## Read Library Foundations

### Summary
This proposes to improve support for Paired-End and Single-End Read Libraries. These objects currently exist in KBase, but are difficult to use for both users and developers. The product here is a set of tools that makes it easy to load, organize, manage, filter, and visualize stats about read libraries.

### Story/Description
KBase currently supports PairedEnd Read Libraries and SingleEnd Read Libraries, but those types are difficult to use. There are multiple representations of each type of read library; there is not much consistency in how they are stored; they cannot be grouped into samples/studies/replicates, they are not easily manipulated or visualized.

The Product is a foundational reads infrastructure that makes it easy to load, organize, manage, filter, and visualize stats about read libraries.

In general, the basic flow of usage would be:
  * User imports a set of reads files and labels the type of reads and other required information.
  * User groups the reads by replicate, study, experiment etc.
  * User views overview summary stats of both the individual reads and files and groups of reads
  * A User can then run Narrative Apps to compute detailed QC or other reports, and view various plots (ideally interactive) of the metrics.
  * Based on the visualizations (or using interactive visualizations) a User will be able to split, merge, subsample, filter, and regroup the reads.
  * A User then creates a sharable narrative with data summaries, plots, markdown descriptions of the data, and links out to Narratives containing the actual QC, filtering, and other data processing steps.

Risks:
The challenging aspects of this PD are to what degree we develop the projects/groups/samples/experiments support, what UI changes we need to support groups.


### User stories
As a user, I want to import a set of reads files and make clear the type of reads on upload.

As a user, I want to group reads objects by various parameters.

As a user, I want to perform QC operations on my reads and view statistical plots.

As a user, I want to share my uploaded reads with other members of my laboratory.

### Narrative Mockup



### Timeline of tasks
  1. Refactor reads objects as necessary for clarity of use, in conjunction with the data API team.
  2. Develop management system for reads - requires UI improvements for assigning data to "groups" which can represent studies, experiments, etc.
  3. Choose and wrap reporting tools for QC of reads or groups of reads (FastQC?). Add visualizers for reports.
  4. Create or wrap tools for modifying reads sets based on QC reports.


### Test plan


### Citations
This will be populated when open-source tools for reads QC are chosen.
