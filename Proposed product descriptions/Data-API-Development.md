### Summary
Add a number of related tools and documentation items to the current Data API repositories, to make it much easier
to create and deploy new "core" Data APIs.

### Story/Description
The Data API is currently implemented for three related core datatypes. Although in many ways the Data API is one of
the most automated components in KBase in terms of testing and documentation, the end-to-end process of creating a 
new API is complicated and would be too difficult for most people outside the Data API team.
It is debatable whether we want Data APIs for every new datatype, but if the Data API concept is to have any utility, 
there should be APIs for the core KBase data types.

This should be done now because the longer the Data API remains a "black art" for a small section of the KBase team,
the more likely it is that new core datatypes and other system components ignore this approach and invent independent
services, complicating the system and duplicating effort.

### User stories

Eustace, a relatively new member of KBase, wants to implement a new Data API for a core datatype needed in his
planned new service. He goes to the Github `kbase/data_api` repository and finds in the README a pointer to
detailed instructions on how to fork the repo and create a skeleton of the Python library and client/server.
This uses standard Python installation procedures. He is able to immediately get started running and testing 
a "hello, world" API that gives him confidence in his development environment. From there, he follows the guidelines
for how to properly build in the base "ObjectAPI" class to specify and implement his interface. When he feels
like he has something working, he submits a pull request from his fork. The lead of the Data API team informs him
that although his API looks OK, he also needs to update the client APIs for JavaScript and Perl (and eventually Java),
pointing him to a document that describes this process including how to structure the PR so the linkages are clear.
These are in separate repositories that he must fork as well, but there is a tool that can automatically generate
all the code from his specification, and tests are automated. Documentation for the new API is all generated from the core Python
repository. He submits PRs for these repos as well, and links them to the main PR. After feedback and associated
modifications in the API interface itself, the PR is approved and a new API is created. It is simple to add the new
service to the deployment scripts. The developer coordinates with the Data API lead and the production devops team to
deploy and test on the usual progression of places ("CI", "Next" and then in production).

### Narrative Mockup
This is a developer-facing feature, and does not have an associated narrative.

### Timeline

* Sprint 1
  * Tasks
    - Perform any re-organization/renaming of repos that was not finished in previous sprints
      to get consistent namespaces for Data API components (this would particularly apply to the JavaScript repos)
    - Create a document that describes exactly how to create a new Data API in the main repo
    - Add scripts needed to streamline/smooth elements of this procedure, including creation of skeletons 
    for code, configuration, and specification files that contain comments on how to modify it for use.
    - Add to this documentation a "best practices" guide that covers data modeling and interface design, to guide
    developers towards creating a more consistent and usable API.
    - Document expected behavior with respect to unit tests and test coverage
    - Make sure new APIs can easily be added to the TravisCI/Codecov setup. Document how to run these tests 
    without having to run the tests on just their new API (not all the APIs in the repo).
    - Test all this documentation and tooling by creating a new "dummy" API
  * Deliverables
     - Documentation and tools for streamlined additions of Python library and client/server APIs
* Sprint 2
  * Tasks
    - Create tools for automatically generating new Perl and JavaScript API clients from new Data API specifications.
    - Document usage of these tools.
    - Document how to run tests for the new clients, and how to add custom code into the wrappers, if desired.
  * Deliverables
    - Documentation and tools for streamlined creation of JavaScript and Perl clients for new API specifications
* Sprint 3 (conservatively; possibly could be done by end of Sprint 2)
  * Tasks
    - Test all documentation and tools on someone who has not been involved with their development
    - Modify implementation as needed to resolve confusion and/or bugfix
    - Link all documentation generated so far to main KBase "developer" documentation pages
  * Deliverables
    - Final, deployed version of documentation and tools
    
### Test plan

Since "we" are the target user, external testing can be foregone in the initial iterations.
Initial iterations of these components will be tested internally by the team with a "dummy" API.

As described in Sprint 3 tasks, the near-final version of the documentation and tools will be tested
against someone who was not part of the earlier sprints to get fresh perspective.

### Citations

* Core library and Python client/server:

   https://github.com/kbase/data_api/tree/develop

* Clients:

  JavaScript: https://github.com/kbase/kbase-data-api-client-js
  Perl: https://github.com/kbase/data_api_perl_clients/tree/develop
