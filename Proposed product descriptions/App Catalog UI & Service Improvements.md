## App Catalog UI/Service

### Summary
The App Catalog UI/Service was just released, but in initial testing there are a number of enhancements that would significantly improve usability both for Users and SDK developers that require changes to the UI and underlying service.  This set of features are grouped together here and can largely each be implemented independently.

### Story / Description
Products:

1.  Release Management Improvement - the current SDK release management tools are too simplistic.  We should be able to ‘tag’ the latest release and easily move that tag among release versions to control what version appears as released/beta.  There needs to be a way prevent specific old versions from running, for instance, if there is a critical security bug uncovered.
2.  Developers should be able to modify release notes per module/app dynamically, and create notes for users.  For instance, to add a warning for a method about a particular bug that was recently discovered.
3.  Beta and old versions of Apps should be visible prominently in the Narrative.  This needs to be dynamic, so that if an app is released, the beta highlight should be automatically removed or if a method is now out of date, it is highlighted with an option to update.
4.  Launch an App in a new Narrative from the App Catalog
5.  From the Narrative methods panel, select and launch an old version of an App
6.  Add an App from an App Catalog to the end of an existing Narrative, then open/refresh that Narrative. (This probably has implementation dependencies on a new Narrative Service).
7.  Improved category-based view of Apps (think Netflix style side-side scrolling of Apps in a category, with expanded views per category)
8.  Better handling of navigation history in the App Catalog (going back in the browser resets app organization settings)
9.  Improved display of stats per App, Module, and User organized into a timeline.  We already aggregate statistics over 1-week intervals, we could show timeline of usage counts, marking release dates and new registrations.
10.  Add multiple levels of admin privileges so that different individuals can review releases, view statistics, and perform system operations (such as setting client groups).  Admin privileges such be dynamic without requiring a catalog redeploy.
11.  Versions of Apps should be pulled directly from module versions, not set independently.

### User Stories
Not done, but some are clearly implied from the Store/Description section.

### Narrative Mockup
Not done.

### Timeline
Up to 4 sprints depending on scope, but should be able to deliver production-ready subset of features in any number of sprints.
To accomplish all these improvements, I anticipate on the order of 3-4 sprints, not including user testing.  Approximately one sprint for release management and dynamic release notes improvements.  One sprint for Narrative related features (launching Apps in new Narratives, highlighting versions of Apps, launching old App versions).  1-2 sprints for interface improvements guided by user testing, such as the improved category view, navigation history, stats displays.

### Test Plan
Some of the ideas here are already based on user testing and experiences with internal users of the app catalog.  After each sprint, however, we should organize a short user testing session with 3-4 people (covering both users and developers) to reprioritize the features.

Unit tests will be added to the catalog backend test framework as needed.  Tests for the front-end App catalog do not exist, but some will be added into the new kbase-ui testing framework.

### Citations
N/A
