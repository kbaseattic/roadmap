# User Data Management and Sequence Reads for Transcriptomics

## Summary

User data management has been identified as a key item to address for a KBase transcriptomics workflow.  Determining a reasonable grouping of data is important for this data management and will be designed with targeted external users under a narrow scope that enables a good user experience with Transcriptomics data and is flexible enough to also work for metagenomics workflows we would like to add to the system.

In addition to User data management, we also need to evaluate the existing Reads data types and determine what changes need to take place to improve the user experience when uploading Reads data to the system, organizing that data, and then utilizing that data for either Assembly or Transcriptomics workflows.

## Description

Targeted external users will be identified with help from UE and others, that will become actual users of the system, bringing in data for transcriptomics analyses.  Other systems such as SRA from NCBI will be reviewed to determine current expectations. Through user testing, mockups, and design sessions, a solid design for organizing and managing data will be developed.  During implementation, frequent interaction with external users will help guide the final product.

## User Stories

- As a user, I need the ability to organize my uploaded sequence data
consisting of 20-40 samples with multiple replicates, including paired
treatment and control samples, into a hierarchy or groups of samples.
