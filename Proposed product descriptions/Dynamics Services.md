## Dynamic services.

### Summary

SDK Developers need an integrated way to define and instantiate
services to support fast access to data especially for UI purposes.

### Story/Description

The SDK has made it relatively simple to run asynchronous jobs but it doesn't currently offer a mechanism to define and instantiate
semi-persistent services on demand.  This would be useful for
cases where you need a service that may need to cache data to
speed up access or the scheduling overhead would interfere with
performance.  For example, if you wanted a Data API
service to support a UI element, having the UI wait for the request
to run through the execution engine would likely hurt the user
experience.

This would allow devs to stand up continuously running service that would be more immediately responsive for UIs or load large files/databases into memory. The developer can write a service that stays up, runs synchronously or asynchronously.
It would directly support UI development, like JBrowse, TreeBrowser, etc.
We should have these functions as clear deliverables.

### User stories

TODO

### Narrative Mockup
N/A

### Test plan

In addition, to having indedpent internal testers use the new mechanism to define a service, we should also use a motivating
use case such as jbrowse to illustrate the usefulness of
supporting dynamic services.

### Timeline

1. sprint for implementation
2. sprint for testing

### Citations

N/A
