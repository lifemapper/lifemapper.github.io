---
title: Updates
image_path: ""
layout: page
---

# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## APIs
Start with generated documentation for the [Lifemapper API](api.html). Below
are updates to the signatures.  All data objects, have the following APIs:

 * get (by object id) returning full object
 * count (with filter parameters)
 * list (with filter parameters) returning atoms or full objects
 
### Input Data objects:
Input data objects also have a Post API.  Some output objects may also be 
posted with metadata rather than computed.

 * EnvLayer
 * Scenario (set of EnvLayers)
 * OccurrenceLayer
 * Shapegrid (layer) 
 * Matrix (one or more layers intersected with a ShapeGrid)
 
### Output Data objects:
 * SDMProject (layer)
 * Shapegrid (layer) 
 * Matrix (one or more layers intersected with a ShapeGrid)
 * Gridset (organizing concept for related Matrices and one ShapeGrid)

### Other 
Other objects have some webservices associated with them, but they are 
non-standard.  

 * EnvType : 
 * Algorithm : Algorithms are described by code, author, parameters, and  
   description om the following [XML file](http://svc.lifemapper.org/clients/algorithms.xml).


|             |          Filters           ||
Object  | userId | squid | afterTime | beforeTime | epsg | afterStatus | beforeStatus |  
 ------------ | :-----------: | -----------: |
Layer       |   X    |         Cell |
OccurrenceLayer      |          *Long Cell*        ||
Content       |   **Cell**    |         Cell |

New section   |     More      |         Data |
And more      | With an escaped '\|'         ||  
[Prototype table]
