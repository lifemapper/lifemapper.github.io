---
title: BiotaPhy Web Client SDM Tutorial
image_path: ""
layout: page
---

# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

BiotaPhy and additional terminology is at [Terminology](/terms)

## Login (or skip to proceed anonymously)

1. Go to the BiotaPhy [web application](https://data.lifemapper.org/biotaphy)
   
1. IF you wish to browse your own data as well as public data, sign in to 
   or sign up for a BiotaPhy account.  In the left pane of the webpage:
    
      * If you do not have a user account, create one by clicking the **sign up** 
        link below the Login button.
      * Once you have a user account, sign in with your username and password.
            
## Species Distribution Modeling

1. To request species distribution modeling on species data in the
   BiotaPhy installation, go to the left pane of the webpage, titled 
   "BiotaPhy SDM | New Project". 
   
1. There are four headings in the right pane.  The first three are input sections, 
   SPECIES DATA, ALGORITHMS, and INPUT LAYERS.  The fourth, SUBMIT PROJECT allows you to submit
   your selections for computation if all three inputs are correctly filled.  

   * **SPECIES DATA**: choose a species for modeling by typing in the first few
     letters of a species name in the 'Search' section.  The page will display 
     a list of scientific species names in the database beginning with those letters, 
     below your typing. Choose your desired species, and repeat for as many 
     species as you want.  Only one set of species points is visible at a time.  
     Switch the visible species by clicking the "eyeball" icon for the species 
     you wish to view. 
   * [ALGORITHMS](/terms.html): choose one or more algorithms to use for creating SDMs for all
     species chosen in the SPECIES DATA tab.  To display choices, hover over 
     the "Add Algorithm" box for a list of all available SDM algorithms 
     available. Hover over individual algorithms to get documentation about
     that algorithm.  When you choose an algorithm, a 'card' will be added to that
     pane.  Hover over the box for a list of parameters filled in with default values 
     for that algorithm. These parameters may be edited. 
   * **INPUT LAYERS**: These sets of input layers are also called 
     [Scenarios](/terms.html).  Choose one set of "Model Layers" and one or more
     sets of "Projection Layers" by checking the radio button or boxes to the 
     right of the descriptions.  Model Layers are for 
     correlating known species occurrences with environmental values 
     (producing the SDM Model).  Projection Layers are
     for applying the SDM model to the same or different regions or time 
     periods and producing potential species distribution maps.  
     Layer sets presented as choices in this tab all have the same layertypes 
     and can be used together.
 
   * **SUBMIT PROJECT**: after SPECIES DATA, ALGORITHMS, and INPUT LAYERS have all
     been filled in correctly, this tab will show them with checkmarks beside 
     them.  Click "Submit Project" and the resulting outputs will be accessible
     for viewing by clicking on the date/time which appears at the top of the 
     list in the left pane.  
       
## NCHC BiotaPhy archive
1. We use 'current' climate data 
   from Worldclim 1.4, soils, landcover, and elevation, at global extent, 
   and 10 minute resolution to model Taiwan species using all points where 
   they have been found, both inside and outside of Taiwan.  

1. We project these models back onto the same 'current' climate, soils, landcover and elevation
   just for the Taiwan region, at higher, 30 second resolution. 
   onto that, and future climate scenarios, all calculated from change 

