# Workspace garbage collection

##Summary:

The Workspace Service (WSS) currently allows deletion of stored data, but that
data is only marked as deleted, still exists in the system, and can be
restored at any time by the user. There is no means to permanently remove data
from the system (much like certain websites of less than stellar repute) beyond
manual database surgery.

Data deletion is non-trivial because [data may possess references to other
data that guarantee access to said data](http://kbase.us/services/ws/docs/fundamentals.html#references).
As such, add a garbage collector (GC) that deletes data without references.

##Story/Description:

Add a GC to the WSS that safely deletes data that is

* marked as deleted by the user
* referenceless

There are many benefits to deleting data:

* The expectation of a user is that deleted data is deleted, not stored forever
* Smaller database index size, increasing performance and reducing memory
  footprint
* Free disk space and lower storage costs

##Approach:

The implementation details are left to the implementation team, but it is
known that a schema change is required. As such:

* Address any other bugs or improvements in JIRA that require schema changes
  at the same time.
    * In particular, provide a separate namespace for deleted objects and
      workspaces.
* Develop and rigorously test a schema conversion utility.
    * Failure of the utility due to a network outage, reboot, or other
      unexpected interruption should leave the database in a state such that
      the utility can be restarted and pick up where it left off.
    * The utility does not need the ability to downgrade an upgraded database
      or an upgrade in progress.



If data contains references to Shock data (via a Handle stored in the
Handle Service), that Shock data will **not** be deleted because the data
does not belong to the WSS.

**Note** that the longer this waits, the more likely it is that a feature is
added to the WOS that makes GC more difficult or impossible. Given that and the
magnitude of the change to the overall architecture it is advisable to add GC
sooner rather than later.

##User stories:
Since deleted data is not currently visible to bench biologists, they will
notice no immediate difference unless contacting a KBase admin to request an
undelete. If the deleted data has no references and was deleted more than
t [time unit]s ago, the data will not be restorable.

If GC is not implemented, Bench biologists and 3rd party developers may notice
performance degradation in the system as database sizes and indexes continue to
grow.

3rd party developers would notice that data eventually disappears from the list
of deleted objects.

##Narrative Mockup:

N/A

##Timeline:

1-2 sprints.

##Test Plan:

Add tests as appropriate to the WSS test suite.

##Citations:

N/A
