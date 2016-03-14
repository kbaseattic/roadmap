## Execution Engine Update - Interface Consolidation

### Summary
KBase currently lacks a centralized execution engine interface, which has generated a significant amount of unnecessary complexity, system instability issues, and lingering problems with job and narrative sharing and security.  There are many possible Execution Engine related projects (HPC execution, resource limits per user, BYOC), but all require (or will be significantly simplified) by consolidation of the existing interfaces into a single execution engine service first.  Proof of delivery will be evident in a new Jobs Dashboard page or widget.

### Story / Description
The current Job related services that are accessed directly through various components are: NarrativeJobService (NJS), NarrativeJobServiceWrapper (NJS_wrapper), NarrativeJobProxy (NJP), User and Job State (UJS), AWE Execution Engine.  Instead, the Narrative and all Job checking operations will be migrated to a single, well-tested service.  The service will handle submission of jobs, listing of current and past jobs, sharing of jobs automatically (as jobs should be attached to a workspace/narrative), fetching job state, fetching job input/output, fetching job logs, and to the extent possible by the job dispatch system (AWE or its replacement) setting some limits on job execution time or jobs per user.  The implementation team will determine the extent to which UJS/NJS/NJP/NJS Wrapper can be reused, salvaged, or completely replaced.

As a proof of delivery, there will be a Job Dashboard page & widget that communicates with a SINGLE backend job service and is capable of:

1.  displaying all running jobs submitted by the logged-in user
2.  display all running jobs visible in narratives by the logged-in user
3.  display all completed and errored jobs sorted by date
4.  Run statistics over time for the user (n runs, which methods, % success, total wall time)
5.  allow selection of any job to indicate, in order of importance: (a) what narrative it was run in, if any, (b) console log output (maybe in a separate page), (c) report objects associated with the job, (d) execution timings, (e) input/output of the method, (f) where it is running (could be specific awe worker node id, or more generally to indicate client groups, or awe vs hpc vs specific cluster)
6.  For admin users, display all running jobs in the system and all recent jobs, with console output available, ideally with some heads up display of available resources
7.  Controls for users to kill jobs they own
8.  Controls for admins to kill any job in the system

And possibly:

9.  Controls for admins to set max number of jobs per user, configurable for each user
10. Controls for admins to set max run time per app, configurable per app or app/user combination.  This may be an option that can be configured by App owners as well.
11. View for queue position for a particular execution group

**Why Now?**  Job sharing is broken in some cases, and even in cases where it works, it is fragile.  Sharing jobs and narratives is a central component of KBase, and therefore needs to be addressed soon.  The current execution engine also makes it difficult for admins and users to track what they have submitted, what is actively running, how long they should expect to wait for a job.  It is too easy now for a single user to submit a series of long running jobs which they cannot cancel and can effectively block the entire system from running anything.  Furthermore, any improvements to allow HPC execution or bring your own compute, both popular feature requests, will be difficult to implement without tackling this product first.


### User Stories
Not done, but some are clearly implied from the Store/Description section.

### Narrative Mockup
Not done.

### Timeline
This is a large effort that will affect how all jobs are executed in KBase.  Total time anticipated is 4-6 sprints for completion of the above tasks, and probably 2 sprints for a first viable working implementation with the minimal subset of features, and probably 3 sprints of development for enough confidence to deploy to production.

1 Sprint - Modify NJS Wrapper API for the Execution Engine and implement first pass at Job Dashboard page to show Running, Shared, and Completed jobs.  Tests at the API level should be possible to populate the Dashboard and show it works in CI.

1 Sprint - Rewire existing Narrative functionality to use the EE for job lookup and submission and console output.  At this point, legacy Apps and most legacy methods will no longer work.  The product should be viable at this point and deployed onto at least CI, possibly next.

1 Sprint - Expanded test coverage plus addition of core features for users/admins to be able to kill jobs, view console output and reports from the Job Dashboard, minimal run statistics aggregated per user.

1-3 Sprints - Remaining features as prioritized later and more extensive testing.   Features here would include more knobs for controlling user/app execution limits, better stats display in the UI, adding the job dashboard to the user dashboard, linking to a notification service, customizations for routing jobs to HPC or alternate clusters, EE status page (current load, queue time, resources available, n active users, etc)

### Test Plan
We will need basic user testing after the first two sprints to prioritize tasks in the third sprint.  Unit tests will of course be required at the execution engine API level covering all exposed methods.  Interactive user testing on CI and next through the narrative over at least a couple months before deployment would be ideal to surface most issues.

### Citations
N/A

