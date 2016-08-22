# Using the APIs or Client Library

.. contents::

.. _SDM experiments : docs/apis/experiments.rst
.. _Environmental Layers : docs/apis/layers.rst
.. _Scenarios : docs/apis/scenarios.rst
.. _OccurrenceSets : docs/apis/occurrences.rst
.. _Projections : docs/apis/projections.rst

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
 
## Single species data and analyses

Data objects containing geospatial data about individual species include:

OccurrenceSet
: Point data representing specimens collected for a single species or taxa.  Data
  contains a location, x and y, in some known geographic spatial reference system.
  Public data in Lifemapper installations are in the 'Geographic' spatial 
  reference system, latitude and longitude in decimal degrees. API documentation
  is at `OccurrenceSets`_ 

Scenarios
: Scenarios consist of a set of environmental layers (i.e. elevation, 
  precipitation, temperature, soil, etc).  For Species Distribution Modeling, 
  researchers often use inputs of 'present day' species points and 'present day' 
  climate and/or other environmental data.  The resulting models can be 
  projected onto hypothetical or predicted environmental data, with the
  same layer types.  An example of predicted environmental data available in 
  the Lifemapper archive is climate data computed for the 
  International Panel on Climate Change (IPCC) for its Fifth Assessment 
  Report (AR5, 2013).  API documentation is at `Scenarios`_ 
  
Projections
: Computed SDM models may be projected back onto the same, or matching 
  environmental layersets (Scenarios) 
  
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

Multi-species data and analyses
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Querying the public contents of a Lifemapper installation
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



