## Dynamic services.

### Summary

SDK Developers need an integrated way to define and instantiate
services to support fast access to data especially for UI purposes.

### Story/Description

The SDK has made it relatively simple to run asynchronous jobs but it doesn't currently offer a mechanism to define and instantiate semi-persistent services on demand.  This would be useful for cases where you need a service that may need to cache data to speed up access or the scheduling overhead would interfere with performance. For example, if you wanted a Data API service to support a UI element, having the UI wait for the request to run through the execution engine would likely hurt the user experience. Likewise for a service supporting narrative method execution by checking parameters before app execution submission, this service would need to run extremely quickly.

This would allow developers to stand up continuously running service that would be more immediately responsive for UIs or load large files/databases into memory. The developer can write a service that stays up, runs synchronously or asynchronously. It would directly support UI development, like JBrowse, TreeBrowser, etc. Currently, the existing KBase service architecture requires a great deal of knowledge about the KBase platform and coordination with the KBase devops team to have the service deployed. Dynamic Services would bypass that process and make it significantly easier to write and launch new services.


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

There is no Narrative component. But we are planning two UI components. First, an extension of the app catalog that would allow developers to browse the existing Dynamic Services. This browser will display basic information, stats and documentation. Second, we will create a new administration interface that will allow the KBase devops team to start/stop services from a registered SDK module and monitor health of running services.

### Implementation Plan

1.	KBase service that can pull any SDK module images, run them, and provide some basic information on what is running and how to connect to them
2.	Connect that to a docker swarm cluster
3.	Use a service registry like consul or etcd wired with docker swarm
4.	Controller UI/API like Rancher or Shipyard if that makes things easier to manage.  We'll start with requiring an admin to start/stop services manually, but ideally we'll have a way to start a service only when a client makes a request, and shut it down after some period of inactivity.


### Test plan

In addition, to having independent internal testers use the new mechanism to define a service, we will also use focus on demonstrating end to end functionality by using a simple example service (FilterContigs) and an existing KBase service (Feature Values)

### Timeline

1. Sprint 1: Demonstrate the dynamic launch of a simple SDK service (e.g. FilterContigs)
2. Sprint 2: Demonstrate use of Dynamic Services using existing KBase service (Feature Values)

### Citations

N/A
