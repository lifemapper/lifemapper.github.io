---
title: Single-species workflow
image_path: ""
layout: page
---
# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

___

## Single-species Analysis

A typical BiotaPhy workflow to analyze data for single species consists of 
computing a Species Distribution Model (SDM), and producing maps of potential
habitat from these models.  Inputs must include:

 * [Occurrence Data](/api.html#/Occurrence_Sets) for a single species or 
   taxa.  Species data may be from the BiotaPhy data library (usually a data 
   aggregator, such as the Global Biodiversity Information Facility (GBIF, 
   www.gbif.org)
 * A Modeling [Scenario](/api.html#/Scenarios) is a set of 
   [Environmental Layers](/api.html#/Layers) corresponding to the approximate 
   time period of the species data (distant past, or current day). BiotaPhy 
   makes available Global Climate data for past, current, and future time periods
   from [Worldclim](http://worldclim.org).
 * One or more *matching* projection Scenarios.  BiotaPhy applies the 
   computed model onto these projection scenarios to creates maps of habitat in 
   which the species may thrive.  Matching scenarios are explained further below.


The inputs are analyzed with the MaxEnt species distribution modeling algorithm to compute 
the relationship between species occurrences and environmental values.  Parameters may be set
to fine tune the MaxEnt algorithm, or the defaults accepted.

User submission for scenarios is not currently enabled.  If you have environmental layers
that you would like to use for SDM computation, we are happy to work with you to assemble
metadata and layers into a package for computations in BiotaPhy.

To request an SDM computation, a user will choose or upload an Occurrence 
dataset, choose a modeling Scenario and one or more projection Scenarios, and optionally 
modify the default MaxEnt algorithm parameters.

