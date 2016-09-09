---
title: Using Lifemapper
image_path: ""
layout: page
---
# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

# Using the APIs or Client Library


The Lifemapper Python Client Library simplifies queries to a Lifemapper
installation by wrapping HTTP requests in the Python language.
Code documentation is at http://lifemapper.github.io.   

The Lifemapper archive contains datasets represented by different data objects 
which contain data and metadata about that data.  Analyses can be performed 
on individual species or taxa, or on large groups of taxa.  

The Lifemapper 'archive' contains SDM maps for species with over 30 data points 
from the Global Biodiversity Information Foundation (GBIF).  The SDM maps show 
areas with similar climatic conditions to areas in which the species has been 
found.

The Lifemapper archive may be queried to find or summarize data, or to 
request computations on existing or user-submitted data.  Users need not login 
to query for existing public data, but must register and login to request 
analyses.
 
### Single species data and analyses

Data objects containing geospatial data about individual species include:

Algorithm
: An algorithm is a procedure or formula for solving a problem.  There are 
  multiple algorithms for computing Species Distribution Models (SDM) which 
  define the relationship between a set of points and the environmental values 
  at those points. Lifemapper provides 12 algorithms

OccurrenceSet
: Point data representing specimens collected for a single species or taxa.  Data
  contains a location, x and y, in some known geographic spatial reference system.
  Public data in Lifemapper installations are in the 'Geographic' spatial 
  reference system, latitude and longitude in decimal degrees. API documentation
  is at [Occurrence Sets](/documentation/api.html#/Occurrence_Sets) 

Scenarios
: Scenarios consist of a set of environmental layers (i.e. elevation, 
  precipitation, temperature, soil, etc).  For Species Distribution Modeling, 
  researchers often use inputs of 'present day' species points and 'present day' 
  climate and/or other environmental data.  The resulting models can be 
  projected onto hypothetical or predicted environmental data, with the
  same layer types.  An example of predicted environmental data available in 
  the Lifemapper archive is climate data computed for the 
  International Panel on Climate Change (IPCC) for its Fifth Assessment 
  Report (AR5, 2013).  API documentation is at 
  [Scenarios](/documentation/api.html#/Scenarios)
  
Projections
: Computed SDM models may be applied, or *projected* back onto the same, or 
  matching Scenarios.  A map created from the projection of this model onto 
  a Scenario is called a *Projection*, and is a file of geospatial data in 
  raster format.  Different algorithms produce projections with different values.  
  The Maxent algorithm produces projections with values denoting the predicted 
  presence as a value between 0 and 1.  Other algorithms produce raster files 
  with only the values 1 (predicted present) or 0 (not predicted present).
  
Experiments
:  Experiments contain a single species 

Species Distribution Modeling (SDM) experiments follow a general workflow.  
A researcher:

  1. begins with input species data and environmental data 
  1. chooses an algorithm and any parameters for computing the model
  1. chooses to project the computed model onto the same environmental
     data, or "matching" data (same type of data and measurement units, 
     perhaps for a different geographic area, or the result of models predicting 
     past or future values) 
     
To request Lifemapper SDM computations, a Lifemapper user may choose inputs from
the public data archive, or upload their own data.  Species data is held in 
'OccurrenceSet' objects in the Lifemapper data archive, and may be queried 
with 'list' or 'count' queries, using filters as the user   

### Multi-species data and analyses

Multi-species analysis allow large scale analyses of the distribution of many 
species.  Scale may refer to the taxonomic, phylogenetic, or geographic breadth 
of the analyses.

Inputs may start with:

 * Species layers.  These layers can be raster or vector format, and can 
   be predicted (i.e. SDM output projections) or other types of distribution 
   or range maps.  
 * Environmental layers.  These layers can be raster or vector format.
 * A grid definition. This defines the geographic bounding box, geographic 
   projection, and grid cell size and shape
 * A phylogenetic tree. This contains a tree in NEXUS format with leaves
   corresponding to each species layer in the analysis.
 * Biogeographic Hypotheses.  These can be in the form of raster or vector files
   describing biogeographic hypotheses for testing.

Data products may include the following matrices:

 * Matrices representing the intersection of layers with the grid:
   * A Presence Absence Matrix, or PAM, which contains the species distributions
     represented as a binary matrix of 0/1 indicating presence or non-presence 
     in a grid cell.
   * Geographic Reference Information Matrix, or GRIM, containing environmental 
     values
   * Matrix representing the Biogeographic hypotheses.
   
 * Matrices representing MCPA calculations 
   * Environmental Correlation
   * Environmental P-Value
   * Environmental R-Squared
   * Environmental R-Squared P-Value
   * Biogeographic Environmental Correlation
   * Biogeographic Environmental P-Value
   * Biogeographic Environmental R-Squared
   * Biogeographic Environmental R-Squared P-Value

### Querying the public contents of a Lifemapper installation



