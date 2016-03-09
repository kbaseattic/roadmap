Summary
=======

Our proposed work will consolidate all code for a new method into a
single repository and allow the developer to test and deploy code into a
shared development environment without coordinating with KBase
personnel. This will make the process of adding new functionality to
KBase significantly faster and easier.

Story
=====

A key factor in the success of KBase is the ease of adding new
functionality to the system by both KBase developers and 3rd parties.
Our KBase core platform has developed and stabilized significantly and
we are now at a point in our development where increasing the scientific
functionality is our most critical need. While there are many obstacles
to adding new functions, the development process as it exists is the
largest. Currently, the process involves cloning several repositories to
build the development environment, submitting code to approximately 4-6
distinct repositories and coordinating with several people to merge and
re-deploy code on development machines. This complexity is holding back
the ability of developers to quickly wrap tools for use in KBase. It is
time to refactor all of these processes and simplify the developer’s
experience.

This work would include: 1) simplifying the code associated with a new
KBase function into a **single repository**; 2) allow for **user
directed deploy and test** the new functionality without intervention by
KBase staff; 3) provide **new UI elements** for tracking jobs, see
runtime generated logs, see summary reports of each job run, automate
the creation of a “method page” containing information on authorship,
usage, tutorials, statistics, etc., and create a browser for these new
methods; and 4) **documentation** for how to use the SDK and general
documents for how develop modules using KBase.

**Single Repository**

We will provide an easy to install command line tool that would generate
a single directory containing all of the files necessary for
development, testing and deployment of a new KBase function. These would
include the KIDL spec file, implementation file, make file, testing
framework, doc templates, and narrative method specs. The command line
tool will allow the user to initialize the module as python, java, perl
or R. The tool will also allow the user to create an example module that
can be immediately registered as a new KBase narrative method and
explore how all the components work together. As much as possible, we
will reduce the amount of redundant information the developer must
provide. Importantly, we will significantly alter the current process so
that synchronous and asynchronous job execution will use the same code
(currently the developer must provide code for as a service and a
separate stand alone script for asynchronous execution).

**User Directed Deploy and Test**

To support these changes on the backend, we will create new services
that will handle the registration and cataloging of new modules. The
user will be able to initiate the registration of new or updated
modules. This will be done through a GUI available in the Narrative so
that module methods maybe immediately tested inside the Narrative. Once
the developer registers a module, the module will be built and deployed
automatically, without the need for assistance from the KBase deployment
team, and the modules methods will be visible within the Narrative. We
imagine the modules having three states: development, beta and
production. There will also need to be Narrative methods for developers
to move modules between these states. We also imagine a new “appdev”
production environment for developers that has its own data stores
(workspace and shock). This is necessary because developers need a
stable environment that is identical to the production environment, yet
they are allowed to create data objects that are incomplete and users of
the production system won’t see unstable development versions of
methods. Users will initially register modules as having the
“development” state. This state indicates that the module is under
active development, is not complete, and not ready for extensive
testing. The “beta” state indicates that the module is nearly complete
and ready for testing of its functionality. These two states exist only
in the “appdev” environment and the developer controls the state. When
the developer is ready to move the code to production, they will be able
to initiate a review process that will involve automated and human
review and ultimately move the module into the production environment
where it will be visible by all KBase users.

A very significant challenge for developers with the current process is
testing. In the new SDK, we will provide a framework for developers to
write tests and run their tests locally. They will not have to deploy
their code on KBase hardware to do their testing.

**New UI Elements**

To enable the new SDK we will create new UI elements. These UI elements
will be for the developers, KBase admins, and KBase the users.

-   **Module Registration UI**. Developers will have an interface to
    register or update modules by using a Narrative method. This method
    will take as input a URL for the code repository and will output the
    log information from the build process.

-   **Module Landing Pages**. A page for each module that contains the
    details and descriptions on the module, author, usage statistics and
    other documentation provided by the developer.

-   **Method Catalog Browser**. A browser available through the
    Narrative Interface and outside the Narrative linked from the KBase
    home page. Users will be able to browse through all Narrative
    Methods and link to the landing pages. This will support search and
    filtering by categories/tags.

-   **Developer Pages**. A modification of existing user pages
    for developers. This page will show the all apps developed and some
    usage stats. The developer will also be able to register new
    functions through here.

-   **Consolidate Job/Output Streams**. When a Narrative Method runs,
    multiple types of output can be created. Currently, there is a job
    status stream, which includes the job id, running/queued status and
    error messages for failed jobs. And there is the output
    data object(s) produced by the method. These two streams are fairly
    disconnected from the input widget. The job information is available
    by navigating to the jobs panel to see it’s running state or to view
    the error message for a failed job. The output data is added to the
    data panel, but data here is not connected to the input box. A
    viewer for the output data is automatically inserted into the
    narrative immediately after the input box. However, only one of the
    output data objects can be visualized and if it is moved or deleted,
    the connection to the input box is lost. We will create a new
    Job/Output box that is automatically connected to the input box
    upon execution. This new box will contain the job information and a
    list of all output objects created by the method. We also propose to
    create two new job output streams, a runtime log and a job report.
    The log will be a console log much like stdout and stderr created by
    a command line program. The report output will be a summary of the
    job that the developer can create at runtime and save as a
    workspace object. These new job output streams will also be included
    in this new Job/Output box.

**Documentation**

The new SDK functions will be documented such that a developer with
little or no previous experience developing for KBase can install the
SDK tools and begin to write a new method. To do this we need
documentation covering the SDK: an overview, installation & setup,
usage, FAQ, and examples. These documents should be in multiple formats,
including text, a web-based format, slides, and videos. Additionally,
developers will also need documentation on KBase itself, an architecture
overview, data types, core platform services APIs, the Narrative, and
documents covering KBase policy. Especially important are the policy and
process documents relating to adding 3rd party tools.

**User Stories**

**Timeline**

Future Work
===========

We imagine that we can extend the SDK to handle UI View Widgets and to
manage Method Reference Data. The viewers can be created in the SDK
generated repository and dynamically deployed into the Narrative. Method
Reference Data we are defining as data initialized by the method when it
is registered and is used when the method runs (e.g. a BLAST database).
Other work would include using the SDK to define workflows or pipelines. 
Upload functions can also be converted to SDK methods.
