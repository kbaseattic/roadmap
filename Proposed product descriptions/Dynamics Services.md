## Dynamic services.

### Summary

SDK Developers need an integrated way to define and instantiate
services to support fast access to data especially for UI purposes.

### Story/Description

The SDK has made it relatively simple to run asynchronous jobs but it doesn't currently offer a mechanism to define and instantiate semi-persistent services on demand.  This would be useful for cases where you need a service that may need to cache data to speed up access or the scheduling overhead would interfere with performance. For example, if you wanted a Data API service to support a UI element, having the UI wait for the request to run through the execution engine would likely hurt the user experience. Likewise for a service supporting narrative method execution by checking parameters before app execution submission, this service would need to run extremely quickly.

This would allow devs to stand up continuously running service that would be more immediately responsive for UIs or load large files/databases into memory. The developer can write a service that stays up, runs synchronously or asynchronously. It would directly support UI development, like JBrowse, TreeBrowser, etc.



### User stories

*	A developer can write a dynamic service with the KBase SDK.
*	A dynamic service SDK repo can be registered by the developer and added to the system/catalog without interaction with the KBase team.
*	The catalog should be able to provide a list of callable methods (with docs)
*	Users should be able to browse the list of available dynamic services.
*	Developers should be able to specify the required resources.
*	Dynamic services should be deployed on hardware matching their resource requirements.
*	SDK should support dynamic services that are synchronous or asynchronous.
*	Admins should be able to start/stop a service for a particular version of an SDK module
*	Admins should be able to monitor the health of running services. Developers should include a get_service_status() method (SDK can provide a basic heartbeat method, devs can add to it if they wish)
*	SDK developers should be able to test a dynamic service locally
*	Dynamic Services system should scale services based on load/usage by adding instances of each service that has high load. And by removing instances of each service/version that isn’t being actively used.
*	Dynamic Services should automatically start a service that isn’t running when a user makes a request of that service.
*	Developers should get basic stats on usage.
*	Developers should be able to specify dynamic services in the same repo as narrative apps.
*	Methods provided by dynamic services should return quickly (~15-60s?) for synchronous use.
*	Dynamic services should have a way to generate service specific clients.
*	Support for service versioning.
*	Support for clients to specify a service version.
*	Be able to specify whether a method can be sync, async, or both (or allow only one and let developer write two different methods method_sync and method_async, if they want both)


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
