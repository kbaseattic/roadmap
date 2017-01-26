# Resolve Genomes and Transcriptomes

## Summary

Refactor the system to stop using Genome in a way that it was not intended and creates problems with other methods and code in the system.
If we do not resolve this, we will continue to have these problems in the system.

## Description

This would involve at minimum:

* Refactoring existing code that depends on transcripts in Genomes
* Building a workflow that allows you to get to a Genome type in order to run FBA or other methods that consume Genome until Data API is more universal
* Replacing the current plant transcripts upload
* Uploader/Downloader/Viewer/etc for transcripts

## Timeline

needs to be scoped

## User Stories

should be defined based on what actual users want to do here

## Citations

n/a
