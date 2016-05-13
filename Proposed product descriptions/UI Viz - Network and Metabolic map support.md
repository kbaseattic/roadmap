#UI Viz Widget Improvement - Network Viz and Metabolic maps

##Summary
Here we are proposing methods and support for visualization, construction, editing, and sharing of dynamically drawn network maps in KBase. This will start with a simple base-widget and associated data types for generic network building, editing, and visualization. These could be gene, compound, reaction, or other networks types. However, we will extend this with a specific set of methods and widgets to support visualization of metabolic pathways. We would preload pathways from KEGG and metacyc, and in the case of KEGG, curate important maps slightly so they look readable when visualized as svg (not painted gifs). The view widgets will show the networks with clickable nodes and edges that show KBase data associated with nodes and edges in the network (e.g. genes, reactions, or compounds). The widgets will also support the painting of other KBase data onto the map, including genomes, models, FBA solutions, TN-seq data, essentiality predictions, and expression matrices.

##Extended description
In more detail, we are proposing to build a series of UI widgets and methods in the narratives to support the visualization of simple networks, and more specifically of metabolic maps in KBase. This will include the addition of four UI widgets: (i) a simple generic network viewer; (ii) a simple generic network builder/editor; (iii) a metabolic pathway viewer; and (iv) a metabolic pathway builder/editor. We will add four methods to the narrative to support the view/editing of simple networks and metabolic pathways: (i) a network viewer that will visualize a network objects where biological entities are nodes and connections delineate interactions and also allows the painting of data onto these biological entities (e.g. expression painted onto genes); (ii) a network builder/editor that allows one to construct a network out of biological entities from other KBase objects, including genomes, models, community models; (iii) a metabolic pathway viewer that enables a user to paint an arbitrary metabolic map with data from a wide range of KBase objects (e.g. genome, model, FBA, expression matrix); and (iv) a metabolic pathway editor/builder, which permits users to customize and share their own maps. We would pre-populate public maps in KBase from KEGG and metacyc, and the narrative methods would automatically enable the visualization of these public maps. However, users will also be able to apply the editing methods to build their own networks and metabolic pathway maps, which they can then share with others. Ultimately, popular publicly available maps can be added to our workspace of public maps for all to use.

Critically, the widget won't just support painting and viewing maps, but one can also click on a node and see charts of data plotted for that node. Generic network nodes will be associated with an entity in KBase, like a genome feature. These labels would be used to support painting of data associated with that feature in a variety of objects on the network. Similarly, nodes in the metabolic pathway maps would be associated with reactions, compounds, and functional roles, which would be used to paint maps with data from genomes, models, FBA, expression, and a wide range of other objects.

Network widgets will be flexibly written to enable their rapid use to visualize data from any narrative method producing network objects. We propose to use a layered design with most generic types and widgets at the bottom, and more specific networks types and widget building on top. For examples: generic network -> [ gene network , metabolic pathway network ].

##Timeline for feature release
+ May 1: deploy a prototype of the most basic network viewer and editor with support for gene networks
+ June 1: deploy prototype metabolic map viewer and editor, as well as public maps from KEGG and metacyc
+ July 1: release four methods in narrative production: (i) metabolic map visualization; (ii) metabolic map editor; (iii) network builder/editor; (iv) network viewer. Also release curated set of visually attractive kegg maps of primary metabolism.

##User stories
+	A user opens up a network builder tool associated with a genome, and manually creates a gene interaction network showing the electron transport chain for their organism. The network is visualized and saved to the narrative as a generic network object.

+	A user clicks on the metabolic pathway visualization method, and they select a genome, a model, two FBA solutions, and two expression matrices. They also select a set of maps of their own making from their narrative for visualization. Finally, they select one of a few publicly available "map-packs" (e.g. KEGG maps, MetaCyc maps, Plant maps). They click "run", getting back an object which contains a count of the number of hits for each object in each map. They select a map from this table, opening the map in another tab and visualizing all 5 selected data objects on the map. They hover over a reaction, showing how FBA and expression agrees for that reaction across all selected data objects in a neatly labeled chart. They use this visualization to find pathways where flux and expression dis-agree and to trace out biological reasons for the disagreement.

+	A user clicks on the metabolic pathway editor method. Then they select from either a publicly available pathway map, or from a pathway map in their narrative. They then edit the map, removing reactions, adding reactions, and re-arranging the layout of reactions, before saving the map and sharing with other users. Ultimately, the KBase team adds the map to a workspace of public maps which we maintain.

+	Visualize expression data associated with gene coexpression networks constructed from co-expression data.

+	Visualize sequence homology networks constructed by the homology service.

##Narrative mockup
Not done yet...

##Network mockup
Not done yet...

##Citations to code sources
+	D3
+	Plotly
