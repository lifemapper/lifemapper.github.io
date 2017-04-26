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
 
Input data objects also have a Post API.  Some output objects may also be 
posted with metadata rather than computed.
 
### Input Data objects:
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
These may be parameter or descriptor types
 * EnvType
 * Algorithm

