#Split the Workspace and Type Database Services

##Summary:

The Workspace Service (WSS) currently consists of an object store organized
into workspaces (WOS) and a type database (TD). Although both services run
in the same service container and share an API, they are not particularly
tightly coupled and separating them into individual services provides several
benefits, described below.

##Story/Description:

The WOS and TD currently share an API and run in the same service container.
However, the TD does not depend on the WOS in any way. The only non-trivial
dependency from the WOS to the TD is defined by
[the TypeProvider interface](https://github.com/kbase/workspace_deluxe/blob/19dbec72e1ac60d665d15563cd9553dc9592c819/src/us/kbase/typedobj/core/TypeProvider.java).

Splitting the WOS and TD into two different services would provide several
benefits:

### Horizontal scaling of the WOS
[At most one TD instance can run per MongoDB database](https://kbase.us/services/ws/docs/knownadminbugs.html).
The WOS does not have this restriction, and so a decoupled WOS can scale
horizontally, which is currently impossible. The WOS must handle a much
larger load than the TD making this highly desirable.

### Share types across environments
Several workspace instances can run against the same type database, sharing
type definitions. For instance, the KBase Next and Production environments
could potentially share one TD, eliminating issues of mismatched types when
testing on Next.

### Offline type validation, object sorting, and duplicate detection
If, as proposed below, the core typed object code (primarily the validator,
as the sorter is already in the
[java_common](https://github.com/kbase/java_common)
repo) is moved to java_common or its own repo with the addition of an
appropriate API, developers could validate, sort,
and produce MD5 digests for their objects prior to attempting to save them to
the WOS, preventing wasted data transfer, processing, and even storage for
invalid or duplicate objects. Offloading sorting onto, for example, NJS workers
will significantly reduce the load on the WOS, as the WOS can then merely check
that the sort is valid.

### Alternate WOS type providers
Separating the WOS and TD would allow running the WOS with an alternate type
provider if desired, as long as the type format could be translated into the
format expected by the WOS.

### Targeted APIs
Currently, if a developer wishes to use the TD, they must also navigate though
the WOS API and vice versa. Splitting the services would provide two separate
APIs that are smaller, more cohesive, and easier to understand.

###Targeted codebases
Similarly, splitting the services into separate codebases would result in
codebases that are smaller, more cohesive, and easier to understand.

**Note** that the longer this waits, the more likely it is that a feature is
added to the WOS or TD that increases their coupling. Given that and the
magnitude of the change to the overall architecture it is advisable to
perform the split sooner rather than later.

##Approach:

Split the WSS codebase into 3 repos containing

* the WOS (suggested repo name: workspace)
* the TD (type_database)
* the typed object validator and associated code (typed\_object\_tools or
  java_common)

Splitting the codebase requires:

* Separation of the code into individual modules
* Deployment code for the TD
* An implementation of the TypeProvider interface that contacts a remote TD
  service
    * WOS side caching will be important for good performance
* Producing separate APIs for the WSO and TD
    * Rewrite TD methods in the WSO to forward to the TD and deprecate said
      methods
* Separating the tests for the WSO and TD
    * Rewriting tests to start new services
* Separating the documentation and rewriting documentation as necessary
* Creation of a new API, tests, and documentation for the typed object tools
    * The API should handle validation, sorting, digests, and loading the
      sorted object
    * Language bindings for the typed object tools. Potentially helpful:
        * https://github.com/kivy/pyjnius
        * http://search.cpan.org/dist/Java/Java.pm
        * http://search.cpan.org/~etj/Inline-Java-0.58/Java.pod

##User stories:
Bench biologists and 3rd party developers would notice that KBase doesn't fall
over when the load on a single WSS gets too high.

A 3rd party developer would encounter:

* Much simpler clients / interfaces for communicating with the WOS and TD
* Tools to validate, sort, and produce MD5 digests for their objects locally or on
  a KBase worker node, simplifying interactions with the workspace, especially
  failure conditions
* The ability to check whether the object they're loading is a duplicate of
  a previous load, and thus abort the load before it starts
* Consistent type definitions across production and test environments if sysops
  determines that is desirable

##Narrative Mockup:

N/A

##Timeline:

1 sprint for a 2-4 person team with the possibility of a second sprint for a
2 person team.

##Test Plan:

Separate existing tests into the three new modules and add new tests as
appropriate.

##Citations:

N/A
