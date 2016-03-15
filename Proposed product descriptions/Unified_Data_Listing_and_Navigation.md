# Unified Data Listing and Navigation #

Matt Henderson, Dan Gunter

## Description

Provide a single API for finding out what data I can access in the
system. This would cover object listings and navigation from workspace,
but also listing "blob" data (too large for the workspace), owned either
through the handle service or shock. Currently, finding objects requires
a combination of searching through the workspace and manually following
links from the workspace objects to the handle service, which does not
follow or preserve the permissions modes. This is very difficult for
developers (UI and service) to understand and use correctly, and even
when the correct call is made it is easy to run into a performance
"trap" where a huge number of results (e.g. all public data) are
accidentally returned.

## Approach

The existing "list\_objects" functions in the Workspace service need to
be enhanced with the following more general operations:

-   Find {workspace objects, blobs} accessible by the current user

    -   define "accessible" to be \_either\_ private sharing or the fact that the object is public

    -   Filter by date shared

    -   Filter results by universal metadata such as owner, object size, and modification date

    -   Sort results by metadata criteria such as object size and modification date, or by internal fields for specific types of objects

    -   Handle large result sets by allowing incremental load ("paging") that would be needed by, e.g., a web interface

-   Deal more intelligently with "public" data, to make navigation easier

    -   As mentioned above, distinguish between data explicitly shared, and public data

    -   Have some 'built-in' knowledge of the system to distinguish between "public user data" and "public KBase reference data".

    -   Stretch goal: be able to further restrict the public user data to users who are "probably collaborators", e.g., by not returning any public data items from users who have never shared any item privately with the user doing the navigation

One solution to this problem would be to modify the Workspace Service to
support higher-level navigation methods. This would require modification
of a core service, though it would have the advantage of giving the new
methods full access to MongoDB's underlying functionality. A drawback
would be that unified access to non-workspace objects would require
extending the workspace code with dependencies on Shock and handle
services (or whatever future versions of the system use in their place).
A lighter-weight approach would be to write a "data API" that layers on
top of the Workspace and Shock, providing the necessary functions. This
approach shifts the complexity from the workspace implementation to the
API layer, with the tradeoff being that the added functionality must use
the workspace interface instead of direct access to MongoDB. Another
potential advantage is that any such layer would be exposed to the user
with the same conceptual and engineering framework as the Data APIs that
are currently supporting the new Genome types. A hybrid solution would
use a Data API layer, but also extend the workspace service to
incorporate some of the underlying functionality more efficiently.

## User Stories

This would be demonstrated using code cells in a Narrative to display
all the workspace objects and blobs owned by the current user, shared
with the current user, and public data.

### *Finding your own objects* 
Bob needs to find a Narrative he was working
on a month ago, on metabolic modeling. He uses the navigation API to
pull up all narratives owned by him, less than 2 months old, with the
word "metabolic" in the title. This gives a short list of half a dozen
narratives (title, metadata, and link) that makes it easy for him to
narrow down to the exact narrative he was thinking of.

### *Finding public (blob) objects* 
Alice has been working with Carol on
some data that was uploaded by Carol's student, Dylan. They have
constructed a number of narratives with the data, but Alice would like
to see the entire dataset. Alice discovers that Dylan uploaded the data
and made it "public" immediately. Alice does not understand, nor care to
understand, the distinction between whether the data is stored in
"workspaces" or "shocks" mentioned in the developer docs, she just needs
to find this data. The navigation API lets Carol find all objects
uploaded by Dylan in a vague time period, filtering by types of data.
This is still a significant dataset, but Carol sorts it by owner and
browses through it to discover a naming pattern that Dylan used and from
there is able to retrieve all the objects easily.

## Timeline

This work will take 2-3 sprints

*  Sprint 1: Design and Prototyping
    *  Paper prototype. Specify the API in as much initial detail as possible, on "paper" (no coding).
    *  User testing. Get 1-2 people external to the team to try out some sample tasks using the specified API. Collect feedback and identify the most important things to change. If it seems necessary, i.e. some glaring issues may have hidden other important problems, repeat this process once the "paper prototype" is modified from the previous round of feedback.
    * Develop prototype. Create an API (using Data API technology) to implement the paper prototype. Minimal testing. Get Python API library and client APIs both working.
    *   Test API prototype, with 1-2 people, in code cells in the narrative.
* Sprint 2-3: Implementation and Deployment
    * Refine prototype. Harden the code with better testing and more stressful queries.
     * Workspace modifications (may take until end of Sprint 2). If necessary, modify Workspace implementation to support performance and functionality requirements of the API
    * Prepare for production. Generate example Narrative that exercises most of the features of the API. Complete documentation, get test coverage >= 70%
    * Final round of UI/UX changes.  
    *  Deployment.  Deploy as an API service in production (along with any Workspace changes).

## Test Plan

Testing has largely been discussed as part of the development process. As noted by many experts, a small amount of testing at the beginning stages of a design is far superior to heavyweight testing at the end. We will of course engage in integration tests as part of the production deployment.

## Citations

n/a
