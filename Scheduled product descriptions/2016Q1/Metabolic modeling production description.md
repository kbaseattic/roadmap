#Improved modeling tools product description

##Summary
Here we describe a series of significant improvements designed to implement numerous features that have been in strong demand by users of the modeling pipeline. These features include: (i) GUI for editing models; (ii) GUI for editing media; (iii) a gapfilling that suggests genes for gapfilled reactions; (iv) model sensitivity analysis which will explain why each gapfilled reaction was added; (v) ability to compare more than two models at once and download results; (vi) improved tools to interpret and understand FBA results;  (vii) enhanced inputs to the gapfilling method, including objective function, bounds, knock outs, and expression data; (viii) enhancements to community modeling including support for mixed-bag models; (ix) port of modeling tools to SDK, and (x) loading biochemistry data user in modeling to KBase SOLR. With these additions, the metabolic modeling pipeline in KBase will become a  more seamless experience, with users being able to curate and refine their models within the KBase platform. Additionally, the outputs from models will be more informative and easier to understand. 

Team lead: Christopher Henry
Team: Chris H, Neal C, Matt D, Janaka E, Jose F, Sam S, Ross O, Bruce P

##Extended description
This product represents a series of eight improvements designed to enhance the overall user-experience and utility of the modeling pipeline in KBase. Here we describe each of the seven improvements in detail:

1.)  GUI for editing models
The is a web interface built as a new method within the narrative, which permits the user to open up a metabolic model from their narrative workspace and manipulate the model, including: (i) adding and removing reactions; (ii) manipulating reactions by changing stoichiometry, changing directionality, and changing gene associations; (iii) adding and removing biomass compositions; and (iv) manipulating biomass compositions by changing stoichiometry.

2.) GUI for editing media
The is a web interface built as a new method within the narrative, which permits the user to open up a media formulation from their narrative workspace and manipulate the media, including: (i) adding and removing compounds; and (ii) changing compound concentrations and flux bounds.

3.) A gapfilling that suggests genes for gapfilled reactions
This is what is know as intelligent gapfill. This involves using weaker blast hits as an additional input for the gapfilling algorithm, driving the algorithm towards solutions for which there is more evidence, and enabling gapfilling to suggest genes for gapfilled reactions.

4.) Sensitivity analysis
Here we want to rapidly find out what biomass components and other metabolic reactions depend on a reaction to function.

5.) Ability to compare more than two models at once and download results
Here, we are adding a tools to support the comparison of more than two models at once, comparison of biomass reactions, and production of an object containing the comparison output in the workspace, which could be downloadable.

6.) Improved tools to interpret and understand FBA results
Here we are proposing tools to facilitate the interpretation of FBA results, including comparison of FBA results with expression data. This would also include data that indicates which biomass components are preventing the model from growing a specific condition. This also includes tools to check the mass balance of a model to determine if a bad flux solution might be due to a mass-imbalance.

7.) Enhanced inputs to the gapfilling method
Here we are proposing several enhancements to gapfilling of metabolic models, including:
+Support for obtaining and managing multiple gapfilling solutions
+Support for thermodynamic constraints
+Better display of gapfilling solutions in the model widget
+Ability to use transcriptomic data to further constraint/improve gapfilling output
+Ability to gapfill a community metabolic model with transcriptome data
+Prediction of thresholds for gene activity in transcriptome data

8.) Enhanced community modeling
Here we are talking about various improvements in community metabolic modeling, including:
+Improve gapfilling of community models that uses transcriptomic data
+Ability to build mixed-bag community models directly
+Ability to compare FBA of community models with expression data

9.) Port of all modeling tools to SDK
Here we are porting all the modeling tools to the SDK, and making various improvements to the interface, including widget improvements and new/improved options on individual methods. Also improving reporting of results to method consoles in narrative.

10.) Loading biochemistry data user in modeling to KBase SOLR
Here we are loading the biochemistry data used in modeling into the KBase SOLR. This enables the data to be used for search in methods like the model and media editor. A later production description will discuss making a landing page for this data.

##Timeline for feature release
1.)  GUI for editing models
Mid January

2.) GUI for editing media
Mid January

3.) A gapfilling that suggests genes for gapfilled reactions
This is what is know as intelligent gapfill. This involves using weaker blast hits as an Late March

4.) Sensitivity analysis
Late March

5.) Ability to compare more than two models at once and download results
Mid February

6.) Improved tools to interpret and understand FBA results
Mid February

7.) Enhanced inputs to the gapfilling method
Mid February

8.) Enhanced community modeling
Mid February

9.) Port to SDK
Mid February

10.) Loading biochemistry data user in modeling to KBase SOLR
Early February

##User stories
+ A user arrives with a genome, and they want to understand how it produces a specific compound of interest from a specific growth condition. First, the user grabs a standard media condition from the database and edits in within a narrative to match their desired growth condition. Then the user builds a model, and gapfills the model. The gapfilling suggests several interesting new annotations for genes that were previously unannotated. The user then specifies a specific reaction to get the gapfilling to activate (the transporter for the desired compound). They repeat gapfilling using their transcriptomic data to further constrain the gapfilling. Again, the gapfilling identifies genes that are important for the production of their compound. The user notes that one of the pathways is wrong. They edit the model within the narrative to correct the prediction. Then they run FBA on the growth condition, maximizing their desired reaction, and comparing the flux solution with their expression data. 

+ A user builds and gapfills models for numerous strains in a microbiome. They compare all the models at the same time, building a large comparative chart of biochemistry. They simulate all models growing individually and compare with transcriptomic data, then they simulate the models within a mixed bag and compartmentalized community, comparing with transcriptomic data. The identify from the transcriptome comparisons key places where the microbes interact within the community.

##Narrative mockup
https://narrative-ci.kbase.us/narrative/ws.5820.obj.1

##Citations to code sources
1.) SCIP
2.) Plotly
