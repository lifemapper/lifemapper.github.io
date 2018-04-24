---
title: Terminology
image_path: ""
layout: page
---
# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

# Species Analysis Terms

SDM
: [Species Distribution Modeling (SDM)](/researcher/sdm) is also known by 
  several other names, including environmental niche modeling, ecological niche 
  modeling, and habitat modeling.  SDM refers to the process of creating 
  mathematical formulas (models) to predict the geographic distribution of 
  species based on where they have been found and the environmental conditions 
  in those locations.
  
Algorithm
: An algorithm is a procedure or formula for solving a problem.  There are 
  multiple algorithms for computing Species Distribution Models (SDM) which 
  define the relationship between a set of points and the environmental values 
  at those points. Lifemapper provides 12 algorithms

Presence-Absence Matrix (PAM)
: A binary matrix containing species distributions of 0/1 indicating presence or 
  non-presence in each grid cell of a region. The matrix may be thought of as a 
  three-dimensional cube, of binary maps, with one layer per species.  The 3-dimensional 
  matrix is flattened into 2 dimensions, with rows representing sites with an x,y 
  coordinate for the center of a gridcell on a map, and columns representing 
  species.  

Phylogenetic Tree
: A data structure containing species names or identifiers for  analyzing 
  evolutionary patterns.  Lifemapper uses phylogenetic trees matching species
  data in a gridset to correlate evolutionary patterns with species 
  distributions and landscape features.  

Biogeographic Hypotheses
: Spatial layers for testing the influence of geographic elements, such as
  geology, drainage basins, etc, on the biodiversity of a landscape. These 
  can be in the form of raster or vector files.
   
MCPA
: Meta-Community Phylogenetic Analysis, briefly explained at 
  [MCPA](/researcher/mcpa).  MCPA is defined by Pedro Peres-Neto in 
  https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1461-0248.2010.01523.x

 
# Lifemapper-specific Data and Parameter Terms

Gridset
: The organizing data structure for a single, or group of analyses. A 
  package may be downloaded for visualization within the Lifemapper web 
  client, or further analyses in other software. 
  
LM Library
: Existing public data in a Lifemapper installation, including input data, 
  such as species points, environmental data layers, and computed SDMs.

OccurrenceSet
: Point data representing specimens collected for a single species or taxa.  Data
  contains a location, x and y, in some known geographic spatial reference system.
  Public data in Lifemapper installations are in the 'Geographic' spatial 
  reference system, latitude and longitude in decimal degrees. API documentation
  is at [Occurrence Sets](/documentation/api.html#/Occurrence_Sets) 

Scenarios 
: Scenarios consist of a set of environmental layers (i.e. elevation, 
  precipitation, temperature, soil, etc).  For Species Distribution Modeling, 
  researchers often choose a set of 'present day' layers ("modeling scenario") as an input 
  along with 'present day' species points.  The environmental data may be 
  global, or regional.  The resulting models can be 
  projected onto the same environmental dataset and/or one predicted for a different time
  period, or one for another region ("projection scenarios").
  An example of predicted environmental data available in 
  the Lifemapper archive is climate data computed for the 
  International Panel on Climate Change (IPCC) for its Fifth Assessment 
  Report (AR5, 2013).  API documentation is at 
  [Scenarios](/documentation/api.html#/Scenarios)
  
SDM Projections
: Computed SDM models may be applied, or *projected* back onto the same, or 
  matching Scenarios.  A map created from the projection of this model onto 
  a Scenario is called an *SDM Projection*, and is a file of geospatial data in 
  raster format.  Different algorithms produce projections with different values.  
  The Maxent algorithm produces projections with values denoting the predicted 
  presence as a value between 0 and 1.  Other algorithms produce raster files 
  with only the values 1 (predicted present) or 0 (not predicted present).

Environmental Matrix (GRIM)
: A matrix of values indicating the mean value of each of multiple environmental variables
  in a regular grid.  The structure is the same of the PAM, but values are not binary.
  GRIM is an acronym for Geographic Reference Information Matrix.

ShapeGrid
: A grid encompassing the area of interest in a Gridset. Species layers are intersected 
  with a ShapeGrid to create a PAM, and environmental layers are intersected with a 
  ShapeGrid to create a GRIM. Intersection parameters define how values (0/1 for a PAM,
  mean values for a GRIM) are computed for gridcells from the values in a species 
  range map or environmental variable map.

Biogeographic Hypotheses
: Spatial layers for testing the influence of geographic elements, such as
  geology, drainage basins, etc, on the biodiversity of a landscape. These 
  can be in the form of raster or vector files.


