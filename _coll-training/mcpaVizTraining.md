---
title: Biotaphy MCPA output visualization
image_path: ""
layout: page
---

# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

Biotaphy and additional terminology is at [Terminology](/terms)

## Retrieve a gridset package

Several pre-subsetted datasets are available from the provided 
USB drive, including the Heuchera genus and the Saxifragales genus.      

## Metacommunity Phylogenetics Analysis

1.	Open the index.html file from one of the output packages included on the USB drive.

1.	Click the “MCPA” link, the first from the left under the package contents.

1.	This interface can take a long time to load if the phylogenetic tree is large. 
   The Heuchera and Saxifraga packages have smaller trees that load fairly quickly.

1.	Use the “Node color” selection box at the top of the left side to choose a 
   predictor that will be used to color the tree.  The left-hand pane will be 
   updated and the tree contained will be colored according to the correlation 
   between the selected predictor and the distributions on either side of the 
   clade.  Brighter colors indicate that the correlation is stronger and darker 
   colors indicate that the correlation is weaker.

1.	Select a clade from the tree, the map will be updated showing red, blue, and 
   purple cells and the tree will highlight descendant species with red for one 
   sister clade and blue for the other.  These are connected as the red cells in the 
   map come from distributions of species highlighted in red, and the blue cells 
   come from species highlighted in blue.  Purple cells indicate that descendants 
   from both sister clades can be found at that location.

1.	The pane below the map will also be updated.  The left side of that pane represents 
   correlation with environmental predictors and the right side is for correlations 
   with biogeographic predictors.  

1.	The color bar beneath the predictor (such as BIOCLIM_12) indicates how correlated 
   the sister clade distributions are with that particular predictor.  The brighter 
   the color and the longer the bar means that the correlation is stronger.

1.	Predictor names that are BOLD indicate that the correlation was found to be 
   significant after permutation testing.

1.	It is most important to look at the environment adjusted R-squared values and the 
   biogeo adjusted R-squared values.  These values indicate if the clade is likely 
   most affected by environmental filtering or historical biogeography.  If both are 
   found to be significant, then there is likely a confounding effect between the 
   biogeographic hypotheses and the environmental data.  If neither is significant, 
   then it is likely that the limiting variable has not been captured.


