# Narrative Scripting

## Summary

We aspire for there to be many different compelling reasons for users to come and use KBase.
Prime among those is for KBase to act as a single stop for accessing data from many different sources
and be able to assess the fitness of that data, compare data, run analyses on that data, and share your results
with others.  To do that for data from, for example 100 organisms, it significantly helps to have a programmatic interface
to what KBase offers, both data and analyses, so that you can enable larger (in scope) and more comprehensive Narratives.
A simple way to enable this functionality in our current system is to leverage the expressive power of
Jupyter code cells along with APIs in KBase to enable users and developers to be able to play with and fully
utilize what KBase offers.

## Description

1. Make sure code cells work the way we want them to.
2. Make sure the Data API has the right methods we want for supporting user workflows in code cells.
3. Make sure that Narrative/SDK methods API has the right methods we want for supporting user workflows in code cells.
4. Code up Narratives ourselves and with users that leverage 1-3 to show useful analyses available from KBase.

## User Stories

As a user, I want to pull genes from 1,000 strains of e.coli and run a series of methods on those genes
to determine which gene will be most effective for my application.  Make it happen, KBase.

As a developer, I want to be able to compare different assembler output for my reads because I suspect that
some of the assemblers produce better sequence results for my organism.  So I want to jump into code cells and
run every assembler method in KBase on my reads, then display a table of statistics about those assemblies that
will help me identify the "best" assemblers.  I want to share this with people in my research group so that they
understand what I did and why I chose this assembler.

## Timeline

### Parallel tasks

#### Code cell validation
#### Data API review and method updates (if any)
#### Narrative/SDK API review and method updates (if any)

## Test Plan

Execute Narrative code cells that exercise the desired functionality.

## Citations

n/a
