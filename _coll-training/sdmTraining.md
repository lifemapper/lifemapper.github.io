---
title: Lifemapper Web Client SDM Tutorial
image_path: ""
layout: page
---

# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Preparation


1. Sign in to Lifemapper
    * Lifemapper top menu option, choose Sign In
    * Create a user account by clicking the **sign up** link in the left of 
      dialog to open a browser 
    * If you are a new user, the app will prompt you to create a new workspace - 
      choose a local drive and create a new directory
1. In all Lifemapper dialogs, click the ? button to display context-sensitive help


## Species Distribution Modeling

### Definitions (in this context)

Algorithm
  : a statistical procedure or method for calculating a model from data inputs 
  
Model
  : a formula relating species data to environmental layerset 
  
Projection
  : an application of the model onto an environmental layerset resulting in a raster map

### Steps

1. First, explore the species archive

    * Click on the LM logo on the right side of the second row of the toolbar;
      this brings up a panel in the lower left
    * To explore some of the contents of this instance of Lifemapper, type 
      in the box, to get a list of species that start with the letters you typed.  
    * When you find a species, double click it to get the point layer, and a 
      list of projections available for that species.  
    * Double click a point layer, or projection layer to add it to the canvas on 
      the right.  They will be automatically colored, if you do this with your 
      own layers, you must do this by hand. 
     
1. To request an SDM experiment:

    * Choose Lifemapper (top menu) → LmSDM: Species Distribution Modeling
    * In the Perform a Lifemapper SDM Experiment dialog there are four sections:
   
        * Name and Description
        * Species Points 
        * Environmental Layer Set
        * Algorithm 
     
   * In the Species Points, type in the middle box to activate auto-complete 
     and choose a species with some points. The Lifemapper Species point 
     set id will be filled in.
     
     * Click the **layerset** icon (it looks like a stack of papers) to the 
       right of the point set id.  This will populate the Environmental 
       Layer Set drop-down box with layersets matching the geographic 
       projection of these point data. These data may be edited in QGIS 
       then uploaded as your own point data.
       
   * Now the Environmental Layer Set box shows the public and (your) user 
     layersets with a matching projection.  Users can upload their own layers, 
     but we will choose from the existing public layersets
     
     * Choose the 'current' (Worldclim 1.4) layerset to model on, project 
       onto that, and future climate scenarios, all calculated from change 
       modeled by Community Climate System, Model, 4.0 (CCSM4), National 
       Center for Atmospheric Research (NCAR) 
       http://www.cesm.ucar.edu/models/ccsm4.0/ for the IPCC Fifth Assessment 
       Report (2013)
       
         * CCSM4-RCP4.5-2050-30sec-SEA: Predicted 2041-2060 Scenario RCP4.5 
         * CCSM4-RCP4.5-2070-30sec-SEA: Predicted 2061-2080 Scenario RCP4.5
         * CCSM4-RCP8.5-2050-30sec-SEA: Predicted 2041-2060 Scenario RCP8.5
         * CCSM4-RCP8.5-2070-30sec-SEA: Predicted 2061-2080 Scenario RCP8.5
       
     * In the Algorithm section, choose an algorithm 
     
         * Advanced tab: algorithm-specific parameters - these are initially  
           filled with defaults.
           
   * Finally, Click the Submit Exp button
   
1. To List your Experiments - and retrieve data and metadata 

    * Choose Lifemapper (top menu) → LmSDM: Species Distribution Modeling → List 
      Experiments
    * Choose experiment
    * Drill down to projections (final maps)
    * Click the Download link – this downloads the projection raster file into 
      the experiment directory within your workspace directory
     
        * The projection is added to your canvas; choose symbolization by 
          double clicking on the layer (or right click then choose Properties)
        * Calculate the min/max, then stretch the values for a better display

