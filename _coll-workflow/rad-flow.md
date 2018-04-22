---
title: Multi-species workflow
image_path: ""
layout: page
---
# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

___

## Multi-species Analyses

A typical Lifemapper workflow to analyze multi-species data is more
complex and flexible. Some or all analysis steps can be executed.  In 
Lifemapper, multi-species analysis inputs may start with:

 * Species layers.  These layers can be raster or vector format, and can 
   be predicted (i.e. SDM output projections) or other types of distribution 
   maps.  
 * A grid definition. This defines the geographic bounding box, geographic 
   projection, and grid cell size and shape
 * A phylogenetic tree. This contains a tree in NEXUS format with leaves
   corresponding to each species layer in the analysis.
 * Environmental layers.  These layers can be raster or vector format.

A simple Range and Diversity experiment could consist of several general steps.  

First, choose a region of interest.  Macro-ecological studies often start with 
continents or even the entire world.  

Second, choose a set of organisms to study.  Researchers may choose species by 
taxonomy, phylogeny, or other attributes, such as ecological, like predator/prey 
relationships or physical attributes, like body size.  Organism data can come 
from any data source, it can be past, present or future, as well as predicted or 
observed.  

Third, intersect each organism layer with a grid for the chosen geographic 
region to create a matrix where each cell contains a value for presence or 
absence of each species in the experiment.  This structure is known as a 
Presence Absence Matrix, or PAM.  

Fourth, compute indices, by-site, and by-species calculations.  

Finally, randomize the PAM, and re-compute indices and calculations to 
determine the statistical significance of the results.

