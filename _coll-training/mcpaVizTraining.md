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

1. Download a gridset package from the Lifemapper service.  For instance, gridset 9 can be found at
   http://gad210.nchc.org.tw/api/v2/gridset/9/package.  This package will only be available for 
   download once all of the outputs have been computed.  For convenience, we have included three output 
   packages on a USB drive.

## Metacommunity Phylogenetics Analysis

1. Open the mcpa.html file from the package in a web browser.

1. The interface displays three panes, one for the phylogenetic tree, one for a map, and one with correlation values.

1. In the tree pane, there is a select box labeled "Node color".  Select a value from this box for a predictor variable 
   to explore.
   
1. Upon predictor selection, the nodes and branches in the tree will change color.  The color represents how correlated 
   each node is with that predictor variable with brighter green and red values incidating higher levels of correlation and
   darker red and green values representing less correlation.

1. Select a node.  Upon doing so, the map in the middle pain will contain the locations where species in that clade are
   present.  Cells will either be red, blue, or purple.  The tree will also highlight species in red or blue.  The red
   species in the tree are linked to the red cells in the map and the blue species are linked to the blue cells.  The
   purple cells indicate that both red and blue species are present at those locations.
   
1. The pane on the right will also update when a tree node is selected.  You will see a list of predictors with the 
   correlation value to the left of each name.  Under the correlation value, the p value is displayed in parentheses.  The 
   p value indicates the frequency that a greater correlation value was calculated in the permutations.  There is also a 
   bar of color under each predictor name indicating how correlated the distribution of the sister clades are with that 
   predictor.



mcpa/index.html
