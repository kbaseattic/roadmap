## SDK and Science Target Functionality - HipMer

### Summary

Users can do a de novo assembly of a plant genome using HipMer.

### Story/Description

The ability to de novo assemble plant genomes would be a unique capablity for KBase.  It would allow KBase to address the needs of an important community plus demonstrate KBase collaborating with major BER center (JGI) and leveraging ASCR HPC resources (NERSC and ALCF).  Part of this effort would be implementing the rquired changes to the SDK infrastructure to support HPC methods.  This method would serve as an example of how other developers could package HPC applications for KBase.

#### Potential Challenges

- HipMer is not currently public released.  KBase would need JGI/CRD to put their source code in a public repository first.

- HipMer requires HPC resources.  KBase would need to extend support for HPC in order to support this method.

### User stories

TODO

### Narrative Mockup

TODO

### Timeline

This work should be done in concert with enabling HPC in an SDK module.  This work is bracketed by access to the HipMer source code.  This is supposed to be publicly released by the end of March.

### Test plan

TODO

### Citations

- Evangelos Georganas, Aydın Buluç, Jarrod Chapman, Steven Hofmeyr, Chaitanya Aluru, Rob Egan, Leonid Oliker, Daniel Rokhsar, and Katherine Yelick. 2015. HipMer: an extreme-scale de novo genome assembler. In Proceedings of the International Conference for High Performance Computing, Networking, Storage and Analysis (SC '15). ACM, New York, NY, USA,  Article 14 , 11 pages. DOI=http://dx.doi.org/10.1145/2807591.2807664
