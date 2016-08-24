---
title: Lifemapper Overview
image_path: ""
layout: page
---

Lifemapper (Lm) is a high-throughput species distribution modeling system and 
set of multi-species analysis tools.  Started in 1999, Lifemapper was created to 
compute, archive and web publish, species distribution models (“SDMs”, also 
known as species niche models and predicted habitat models) using all available 
online species occurrence data. Using the Lifemapper platform, known species 
localities georeferenced from museum specimens are combined with climate models 
to predict a species’ “niche” or potential habitat availability, under current 
day and future climate change scenarios.  The LmSDM component computes these 
single-species predictions.  

Lifemapper Range and Diversity, “LmRAD", extends Lifemapper from creating 
single-species predictions to large-scale multi-species, landscape-level 
analyses.  The LmRAD component calculates multi-species biodiversity analyses 
by creating a binary presence-absence matrix (PAM) for a large number of species 
from SDM outputs or other species range maps, then computing a number of 
biodiversity measures from it. 

The Lifemapper platform is a large but modular web services-based system of 
three core software components: (1) LmServer for data management and 
communications; (2) LmCompute for calculations; and (3) client applications 
including a Lifemapper plugin to the open-source geographic information system, 
QGIS, and a web site. The LmCompute and LmServer modules are both involved in 
modeling operations. LmCompute instances request jobs from LmServer, execute 
them, then post the model results back to LmServer where data are written to 
storage and metadata to the PostgreSQL database. Two applications on LmCompute 
underlie SDM calculations: openModeller and MaxEnt, while all LmRAD calculations 
are performed by Lifemapper code. From LmServer APIs and a Python client 
library, a user can obtain original and computed data using the Lm website or 
the QGIS workstation GIS environment.
