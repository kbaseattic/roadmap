## Dynamic services.

### Summary

SDK Developers need an integrated way to define and instantiate
services to support fast access to data especially for UI purposes.

### Story/Description

The SDK has made it relatively simple to run asynchronous jobs but it doesn't currently offer a mechanism to define and instantiate semi-persistent services on demand.  This would be useful for cases where you need a service that may need to cache data to speed up access or the scheduling overhead would interfere with performance. For example, if you wanted a Data API service to support a UI element, having the UI wait for the request to run through the execution engine would likely hurt the user experience. Likewise for a service supporting narrative method execution by checking parameters before app execution submission, this service would need to run extremely quickly.

This would allow developers to stand up continuously running service that would be more immediately responsive for UIs or load large files/databases into memory. The developer can write a service that stays up, runs synchronously or asynchronously. It would directly support UI development, like JBrowse, TreeBrowser, etc. Currently, the existing KBase service architecture requires a great deal of knowledge about the KBase platform and coordination with the KBase devops team to have the service deployed. Dynamic Services would bypass that process and make it significantly easier to write and launch new services.

#### Developer User Concept of Operations [new service creation]

1.	Install KBase SDK
2.	Write and locally test service with SDK.
3.	Commit code to publicly available code repository.
4.	Register new service with KBase service catalog using UI or kb-sdk command-line, specify resource requirements, and request deployment.
5.	Wait for review and deployment notification.
6.	Test service, use service, observe usage stats, etc.

#### KBase System Admin Concept of Operations [new deployment]

1.	Get alert for new deployment requests.
2.	Review code.
3.	If code passes review and resource requirements can be met, use API to allow service to be deployed.


#### KBase Platform Concept of Operations [registration]

1.	On submission of new service repositories, build docker container.
2.	If container builds, run tests.
3.	If tests pass, add container to docker image repository.
4.	Send alert to Sys Admin for review.
5.	If service passes review and is marked for deployment, status is updated and service is available through service catalog and visible in service browser UI.
6.	Service is published in service list.

#### KBase Platform Concept of Operations [service call]

1.	A properly structured request for a published service arrives.
2.	If service is already running
    1. forward request to service
    2. record usage statistics
3.	If service is not running
    1. service is started & added to router
    2. request sent to service
    3. record usage statistics

#### KBase Platform Concept of Operations [service balancing]

An automated load balancing system will not be part of this initial product feature set.

#### Service Catalog UI Concept of Operations [developer]

1.	Developer searches for service call matching needs.
2.	Developer can browse list of relevent matching service calls.
3.	Developer can select details on a service call and find: description text, example usage, run time stats, link to the code, etc.
4.	If the developer cannot find an appropriate service call for her needs, she can use a "Manage/Register" control page to add a new service.

#### Admin Service Catalog UI/API Concept of Operations

1.	Admins can view usage statistics of individual services.
2.	Admins can view overall resource utilizations levels.
3.	Admins can start or stop services in response to demand.

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


SDK modules are deployed and run as Docker containers.  We also plan to run dynamic services from Docker containers.  Therefore we need a Docker orchestration and execution framework for services.  There are a number of potential frameworks for Docker orchestration, and options for running Docker Swarm directly, but Rancher (open source, Apache License) appears to have the best balance of usability, features, and stability.

The plan is to use Rancher to dynamically start, stop, distribute and monitor dynamic services.  Configuration of service ports/urls is automatically handled by DNS created by Rancher.  The Rancher DNS will be used in conjunction with Nginx to correctly route requests.

Dynamic service registration will share the same KBase SDK module registration process.  We will explore to what degree we should mark modules/methods as something that can run as a dynamic service.  On registration, we will need to forward some information to Rancher to mark the new available container.

Additional service methods will be added to either the Catalog or a new stand-alone service that allows clients to automatically fetch a dynamic service url from a module name + semantic version.  The service will also allow admins to directly start/stop services.  All users will be able to list running services and check the status/health of those services.  If that works well, we will add in the dynamic component so that a client can start and call a service that isn’t already running, and inactive services are automatically reaped.  This functionality will likely be part of the new service or the catalog.

A complete solution for client distribution for specific services is not an immediate priority, but will first likely be available through the Catalog service.  Until client distribution is further investigated, we will have generic clients allowing developers to call any dynamic service method and version, and of course any generated clients in SDK module git repos will continue to be available.

### Test plan

In addition, to having independent internal testers use the new mechanism to define a service, we will also use focus on demonstrating end to end functionality by using a simple example service (FilterContigs) and an existing KBase service (Feature Values)

### Timeline

1. Sprint 1: Demonstrate the dynamic launch of a simple SDK service (e.g. FilterContigs)
2. Sprint 2: Demonstrate use of Dynamic Services using existing KBase service (Feature Values)

### Citations

N/A
