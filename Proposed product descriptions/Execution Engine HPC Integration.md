# Execution Engine HPC Integration

## Summary
We propose to extend our backend execution engine with HPC capabilities. This will address the log jamming and lack of scalability in the execution engine and the need to enable HPC job execution for shorter time-to-solution and greater throughput. This will also lay the groundwork for supporting very large-scale computations that can be KBase's selling point but are not possible with the current execution engine.   

## Story/Description
Today, the KBase narrative jobs run on individual virtual machines with limited computing resources (CPU, memory and I/O). This results in unsatisfying time-to-solution for many user needs. For example, a production genome assembly job currently runs on 3 CPUs, even though many assembly algorithms can take advantage of multithreading and potentially reduce the walltime for a big isolate genome to 3 hours from 2 days with more CPUs. RNA-seq analyses for microbes and plants routinely involve tens of conditions, each of which consists of multiple replicates. The computations for these samples are executed sequentially in the current system even though they are mostly independent of each other. This means a parallel RNA-seq pipeline could reduce analysis time by 100X. There are other analyses such as large metagenome assembly that are simply impossible due to the memory limit on a single node. 

We plan to build an HPC-capable execution engine to address these needs. It will leverage the existing excution engine, the research on container and scheduling at HPC centers, and the HPC allocations KBase already has. We will design a system with minimal user-facing changes and is also easy to use by the developers. We will first exploit node-level parallelism to support batch jobs. This capability will greatly reduce the queuing and execution time. We will also build additional features such as smart resource estimation through inference on collected metadata of past jobs. Our ultimate goal is to fully leverage the distributed memory, fast interconnect and high-performance I/O on the HPC systems to scale very large-scale compututation such as terabase assembly and cross-domain homology. 

## User stories
User 1 would like to run batch assembly of 100 microbial genomes.  
User 2 would like to do RNA-seq analysis on 100 samples.
User 3 would like to run an NR similary search across 2000 uploaded contigs.  
User 4 would like to run 5000 FBA models.  
User 5 would like to do an assembly of a very large metagenome (1TB) using distributed-memory tools such as HipMer on as much computing resource as possible.

## Narrative Mockup
HPC version of the RNA-seq pipeline in one narrative method
HPC version of the genome assembly method

## Timeline
#### Sprint 1 
1. Evaluate options for execution engine. 
2. Begin implementation plan. 

The execution engine needs to support docker images on HPC and be integrated with the existing queuing and logging systems. The basic workflow is to download an image, upload and the image to the HPC's private docker hub, register with HPC, compose a job script with the metadata from AWE, submit the job with the HPC, and monitor and report back the job status and logs. We will evaluate multiple options for each step as well as explore existing systems such as shifter, DRMAA and NEWT. 

#### Sprint 2
1. Complete implementation plan
2. Build prototype implementation of the EE. 

#### Sprint 3 
1. Deploy EE on test environment
2. Deploy EE on test HPC environment (NERSC first and then Beagle) 
3. Build a scheduling and resource estimation system

#### Sprint 4
1. Port example workflow methods to HPC
2. Correct any problems identified with method execution

The initial goal is to realize the following three types of scalability: (1) node-level parallelism (target method: single genome assembly with many threads), (2) many-task computing (target method: batch FBA of hundreds of input), and (3) end-to-end pipeline refactoring (target pipeline: RNA-seq).

#### Sprint 5
1. Performance tuning
2. Update developer documentation

## Test plan
1. Test each user story after the sprint that implements the functionality
2. Scalability testing will occur during sprint 3/4

## Citations
N/A
