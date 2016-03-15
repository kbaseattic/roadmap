# Unified Data Sharing

## Summary


Provide a sharing API that enables a developer to share any specified
data and Narratives on behalf of one or more users. Sharing should
enable the correct permissions specified by the user, including read
only to specific users, read only for public access, and read/write to
specific users. Sharing should be simple to understand and explain to a
user and be consistently applied according to documented behavior.

## Description


Categories of data sharing would be:

-   private data to one user (my data)

-   private data shared among some users (shared with me)

-   public data shared by KBase (shared by KBase) e.g., reference data

-   public data shared by users (shared by users)

## User Stories


As a KBase user, I want to share my Narratives and data with specific
KBase users.

As a KBase user, I want to share my results so that they are visible to
anyone that accesses KBase.

As a KBase developer, I want to make reference data publicly readable by
KBase users, but distinct from public data shared by regular KBase
users.

## Timeline


Actual timeline should be scoped by the stakeholders and implementation
team. This is a proposed staging that would take place between 4-5
sprints.

-   Sprint 1

    -   Recruitment of KBase users as stakeholders

    -   Stakeholder testing with existing system and sharing

    -   Agree on desired behavior

-   Sprint 2

    -   Agree on API interfaces and prototype with minimal TravisCI tests and documentation

    -   Have stakeholders try the API from KBase CI and provide feedback

-   Sprint 3

    -   Determine core test cases and ensure &gt; 50% coverage in TravisCI

    -   Implement changes and documentation updates based on stakeholder feedback

    -   Have stakeholders evaluate updates from KBase CI

-   Sprint 4

    -   Narrative refactored to use sharing API

    -   Migrate to KBase Next and perform integration tests, sharing Narratives and data and running workflows

    -   Assuming no issues found that would prohibit production deployment, schedule for deploy to production

-   Sprint 5

    -   Any cleanup needed that would prevent a production deploy

    -   Any final updates that would enhance the product for users/developers

    -   Schedule for deploy to production

## Test Plan


Unit tests must be runnable in TravisCI and cover all edge cases to
ensure privacy will not be compromised and sharing actually works. There
must be at least 50% code coverage as demonstrated from TravisCI.

Integration testing will be performed manually using Narratives and
KBase data, executing existing workflows in the system to verify that
behavior is consistent.

## Citations


n/a
