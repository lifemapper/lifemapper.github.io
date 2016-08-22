Lifemapper
==========

.. contents::

Overview
~~~~~~~~
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

Data and Functions
~~~~~~~~~~~~~~~~~~
The Lifemapper software can be logically thought of as having two primary 
resources: geospatial data and analysis tools. 

The first, geospatial data, consists of a library of species and environmental 
data, including climate data (elevation, and observed climate, and predicted 
past, future climate), specimen occurrences (known locations where an organism 
has been collected), and computed maps of geographic locations with similar 
climate and elevation where the species could thrive. All of these data may be
browsed, queried, and downloaded using the Lifemapper web services.

The second, analysis tools, are for analysis of both single-, and multi-species 
datasets.  Single-species analyses are at the heart of the data library
described above, and are encompassed in a module named Lifemapper Species
Distribution Modeling, or LmSDM. Multi-species analyses are contained by the 
module named Lifemapper Range and Diversity, or LmRAD.  

Installation
~~~~~~~~~~~~
The Lifemapper software can be installed on physical or virtual hardware that 
supports Rocks 6.2 cluster management toolkit (http://www.rocksclusters.org/)  
which is built on the CentOS 6.6 Linux operating system. A minimum of 16GB RAM 
is recommended, and storage space adequate for the computations you will 
execute.  The default installation has low resolution (10 min) climate data,
global extent, and a subset of species data from GBIF.  It contains about 7 GB 
of input data and will create by default, about 50 GB of output data.  Any 
compute nodes will need about XXGB of space for computations.

The most recent Lifemapper software is available as two Rocks rolls, one for 
the LmServer component, one with the LmCompute component.  Each contains a 
README file with instructions.  The third component, client applications, 
are intended to query a Lifemapper installation for data and analysis requests.  
The Python client library is this package.  The Lifemapper plugin to the open 
source GIS package QGIS (www.qgis.org) can be downloaded  
from the QGIS plugin repository.  

Query
~~~~~
The 

Future Directions
~~~~~~~~~~~~~~~~~
As part of a collaboration with San Diego Supercomputer Center through the 
Pacific Rim Analysis and Grid Management Assembly (PRAGMA), we recently ported 
Lifemapper to the Rocks Cluster Distribution to run on physical or virtual 
clusters. This change greatly stabilized and hardened our software, but our
local resources struggle to handle much larger scale 
experiments.  As part of an ongoing proof-of-concept experiment with Harvard 
University, we are running multiple SDMs on North American data for the 
kingdom Plantae.  Our continuing work with SDSC has led us to the conclusion 
that deploying our software on a virtual cluster on SDSC’s Comet cluster would 
leverage both our existing Rocks-based software stack, and also the virtual 
cluster support unique to Comet.  

