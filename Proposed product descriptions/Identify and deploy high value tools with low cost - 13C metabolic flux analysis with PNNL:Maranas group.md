#Identify and deploy high value tools with low cost - 13C metabolic flux analysis with PNNL/Maranas group

##Summary
The Maranas group and a group at PNNL have a variety of tools for predicting pathway flux from 13C labeling experiments. We will work with these groups to use the SDK to load these methods into KBase. First, we will add a data type for NMR spectra of labeled metabolites, and the PNNL EMSL team will add a push-to-kbase support for these spectra from EMSL. We will also add metabolite labeling pattern abundances as another new data type. The PNNL team will add a method to convert NMR spectra into metabolite labeling pattern abundances. We will also have an upload for this data type. The data type will be used to store observed labeling patterns in product molecules, but also the labelling patterns provided in media. We will load atom mappings from Costas' MetRxn and MetaCyc into our database, mapping to our biochemmistry, and making the export of atom mappings for metabolic models available. Then the PNNL and Costas's team will help us add a 13C MFA tool which will take a model, a labeling pattern for media, a media, and a labeling pattern for end-point metabolites as input, and it will produce a predicted flux profile in the form of an FBA object as output. This will serve as input to kinetic modeling, described in another PD. 

##Extended description
To be worked out with Costas and PNNL.

##Timeline for feature release
To be worked out with Costas and PNNL.

##User stories
+	A EMSL user runs 13C labeling experiments, does NMR analysis, loads the specta to KBase, builds a model of their organisms, gapfills, then loads labeling patterns used as inputs to their experiment (50% ratio of 100% labeled glucose/unlabeled glucose). They run the fluxomics getting predicted flux profiles, but the profiles don't match well. The user refines their model, improving the fluxomics fit and producing a high quality flux estimation. They run additional experiments to discover an apparent bottleneck preventing the flux through their product pathway from rising with overexpression of the pathway genes. 

##Narrative mockup
Not done yet...

##Network mockup
Not done yet...

##Citations to code sources
To be worked out with Costas and PNNL.