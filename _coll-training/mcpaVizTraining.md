---
title: Lifemapper MCPA output visualization
image_path: ""
layout: page
---

# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

Lifemapper and additional terminology is at [Terminology](/terms)

## Retrieve a gridset package

Several pre-subsetted datasets are available for download, or from the provided 
USB drive, including the [Rubiaceae](http://yeti.lifemapper.org/dl/Rubiaceae.zip) 
family of flowering plants, and the 
[Geometridae](http://yeti.lifemapper.org/dl/Geometridae.zip) family of moths.      

## Metacommunity Phylogenetics Analysis

1. Open the Lifemapper web client, by opening the 
   Rubiaceae/output/gridset-10-package/index.html file in a web browser.  
   This will allow you to browse the inputs and explore the outputs of 
   multi-species, and phylogentic analyses on this subset of the Taiwan data 
   library.

1. The interface displays three panes, one for the phylogenetic tree, one for a 
   map, and one with correlation values.


1. In the tree pane, there is a select box labeled "Node color".  Select a value 
   from this box for a predictor variable to explore.
   
1. Upon predictor selection, the nodes and branches in the tree will change 
   color.  The color represents how correlated each node is with that predictor 
   variable with brighter green and red values incidating higher levels of 
   correlation and darker red and green values representing less correlation.

1. Select a node.  Upon doing so, the map in the middle pain will contain the 
   locations where species in that clade are present.  Cells will either be red, 
   blue, or purple.  The tree will also highlight species in red or blue.  The 
   red species in the tree are linked to the red cells in the map and the blue 
   species are linked to the blue cells.  The
   purple cells indicate that both red and blue species are present at those 
   locations.
   
1. The pane on the right will also update when a tree node is selected.  
   You will see a list of predictors with the 
   correlation value to the left of each name.  Under the correlation value, 
   the p value is displayed in parentheses.  The 
   p value indicates the frequency that a greater correlation value was 
   calculated in the permutations.  There is also a 
   bar of color under each predictor name indicating how correlated the 
   distribution of the sister clades are with that predictor.


