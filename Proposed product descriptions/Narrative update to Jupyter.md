**Summary**  
The Narrative Interface is currently backed by IPython v.1.2.1. This update will result in a release of the Narrative that will be backed by Jupyter Notebook v.4.1.0. This will result in:  
  * Increased stability and security of the server.
  * Adoption of countless changes that have happened in the IPython/Jupyter notebook community in the past few years.
  * Improved ability for users to use Jupyter code cells to access KBase functionality, and also use commonly available libraries (e.g. Plot.ly, matplotlib, pandas, numpy, R, etc.).  

This product will also include a tighter coupling between the Narrative Interface and other aspects of the KBase user interface. This includes a clear integration with a host of interactive display widgets for interacting with data objects in the Narrative, and tools for third party developers to build their own widgets in the KBase SDK.

**Description**  
The Narrative Interface (NI) was originally based on the IPython Notebook. Development of the NI started in the early release days of the IPython Notebook, circa release 0.8-dev. At that time, we had requirements that forced us to maintain a fork of the IPython Notebook’s front end code and build against that, effectively locking us to version 1.2.1 of IPython. In the meantime, the IPython project grew by leaps and bounds and has now become the (language-agnostic) Jupyter project.

At the same time, other non-Narrative KBase interfaces were developed and grew into their own applications, including data landing pages, and the search interface.

The focus of this update is to refactor the Narrative Interface in the following ways. First, it will be rebuilt to make use of the massive number of changes and community adoption available in the Jupyter Notebook v.4.1.0. As a part of this update, the KBase Narrative code will be decoupled as far as possible from the Jupyter Notebook, making future updates easier. Having the ability to keep in step with the Jupyter team will be a great benefit for KBase users. This will eventually give access to multiple kernels for more computational users to directly access KBase resources through the API, and it will enable third party developers who may have familiarity with Jupyter to use that experience to develop for KBase.

In parallel with the Narrative update, other user interface tools will be created to allow KBase (and third party) developers to build and submit interactive widgets for consuming and displaying data objects. This entails a complete UI developer toolkit and API for building widgets using various JavaScript libraries. At first, these components will be stored in the KBase organization repositories in Github, but with coordination with the SDK efforts, will expand to the Module Catalog service (not as a part of this initial product).

**Timeline**  
  * January 13 - Narrative/Jupyter becomes available on ci.kbase.us for integration testing.
  * January 15 - Updated kbase-ui repo becomes available on ci.kbase.us for integration testing.
  * Mid-February - Narrative/Jupyter and KBase-UI updates are released to production.
  * March - Narrative/Jupyter/KBase-UI architecture documentation is made available.

**User Stories**  
User ABC is an experienced Jupyter user and computational biologist who wants to import his workflow into the KBase environment. ABC creates a new Narrative and tests his workflow in the KBase ecosystem, using the KBase data API in code cells, and up to date versions of matplotlib and the IPython kernel for testing. 

User XYZ wants to create a landing page for her new chromatography data type. She already has a KBase developer account, and an SDK module to support her chromatography analysis tools, so she downloads the kbase-ui developer environment from Github. She follows the documentation and uses the pre-installed API packages to locally build and test her widget against data in the Application Developer environment. She then updates her SDK module, where the new landing page becomes available in KBase.
