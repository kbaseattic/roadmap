# Improved Data Visualizations

## Summary

KBase has a need for improved data visualizations. Many viewers provide
dense table outputs that are filled with information, but are difficult
to comprehend as a whole or quickly browse or evaluate from. Having a
few plot types that most data could be mapped to would help users
understand the fitness of data and results of analyses. The additional
challenge here is that data can be large enough that simply pulling back
all the data elements and attempting to plot everything is problematic.

## Description

Rather than attempting to provide plots for every possible data type
combination, instead it makes more sense to standardize the input to a
plot. Using dataframes and/or matrices, it is possible to represent data
in a more uniform way that could be used as input to one or more plots.

The goal here would be to provide a set of API methods and visual
widgets that produce/consume dataframes and/or matrices.

For large data, there will need to be a data reduction mechanism
available from the API, and it should be possible to “stream” or request
data in chunks. All data sizes will benefit from this, but it is a
critical issue for large data.

### Target plot types

-   Scatter

-   Line

-   Bar (vertical and horizontal)

-   Heatmap

## User Stories

As a KBase developer, I want to be able to create a heatmap plot for
data from different services in the same way, without needing to build
several different widgets.

As a KBase user, I want to be able to see a visual plot that summarizes
my data.

## Timeline

Actual timeline should be scoped by the stakeholders and implementation
team. This is a proposed staging that would take place in up to 4
sprints.

-   Sprint 1

    -   Gather stakeholders and agree on initial plot targets and functionality

    -   Demonstrate a single plot type using a dataframe produced by an API method

-   Sprint 2

    -   Produce dataframes/matrices from multiple API methods

    -   Demonstrate reuse of the same plot type for other API methods that produce a dataframe

    -   Stakeholders evaluate from KBase CI environment and provide feedback

-   Sprint 3

    -   Incorporate feedback from stakeholders

    -   Integration testing in Next

-   Sprint 4

    -   Expand plot types

    -   Evaluate/Test/Deploy

## Test Plan


### Unit tests

The API functionality should have unit tests in TravisCI that provide at
least 50% coverage of the new functionality.

### Integration tests

Plots should be visible from a KBase UI, such as Landing Pages or
Narrative. Manual testing of these plots on different and large data
should be performed and should appear consistent.

## Citations

n/a
