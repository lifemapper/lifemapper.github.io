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

A typical Lifemapper workflow to analyze data for single species consists of 
computing a Species Distribution Model (SDM), and producing maps of potential
habitat from these models.  Inputs must include:

 * [Occurrence Data](/api.html#/Occurrence_Sets) for a single species or 
   taxa.  Species data may be from the Lifemapper data library (usually a data 
   aggregator, such as the Global Biodiversity Information Facility (GBIF, 
   www.gbif.org)
 * A Modeling [Scenario](/api.html#/Scenarios) is a set of 
   [Environmental Layers](/api.html#/Layers) corresponding to the approximate 
   time period of the species data (distant past, or current day). Lifemapper 
   makes available Global Climate data for past, current, and future time periods
   from [Worldclim](http://worldclim.org).
 * One or more *matching* projection Scenarios.  Lifemapper applies the 
   computed model onto these projection scenarios to creates maps of habitat in 
   which the species may thrive.  Matching scenarios are explained further below.
 * An [Algorithm](/api.html#/Algorithm) for computing the relationship between 
   species occurrences and environmental values.  Algorithms with
   code, author, parameters, and description is located in the following
   [XML file](http://svc.lifemapper.org/clients/algorithms.xml).

Each individual Environmental Layer must have a 
[Type Code](/api.html#/Type_Codes) which allows the software to identify the 
type of layer when *projecting* the model back onto the same or matching 
scenario. Scenarios *match* if they contain layers with the same type codes. 
Layers sharing type codes must represent the same type of environmental data, 
with the same units of measurement.

To request an SDM computation, a user will choose or upload an Occurrence 
dataset, a modeling Scenario, and one or more projection Scenarios, choose an algorithm, and optionally modify 
the default algorithm parameters.

Currently these uploads and the SDM request happen in multiple steps, but 
the next version of the API will allow all inputs and parameters to be 
defined and uploaded at the same time.

