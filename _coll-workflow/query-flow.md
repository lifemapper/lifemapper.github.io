---
title: Biotaphy Analyses
image_path: ""
layout: page
---
# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Querying the contents of a Biotaphy installation

Aggregate queries will give you a sense of the size, depth and breadth of a
Biotaphy public archive.

To query input and output SDM data, filtering by various attributes, use the 
Python Client Library 
[SDM Query functions](/docs/clientLibrary/classLmClient_1_1sdm_1_1SDMClient.html).
to get counts of objects.  

Digging into the parameter documentation will lead to the constants that define 
status and the input format required for date filters.  Algorithms may be 
queryed in the same way to produce a list of algorithms present in the database 
and optionally filter models on algorithm code.  Algorithms with
code, author, parameters, and description is located in the following
[XML file](http://svc.lifemapper.org/clients/algorithms.xml).