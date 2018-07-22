---
title: Request Multi-Species Analyses
image_path: ""
layout: page
---


Biotaphy and additional terminology is at [Terminology](/terms)

## Login (or skip to proceed anonymously)

1. Go to the test Biotaphy [web client](http://notyeti-191.lifemapper.org/boom)
   
1. IF you wish to browse your own data as well as public data, sign in to 
   or sign up for a Biotaphy account.  In the left pane of the webpage:
    
      * If you do not have a user account, create one by clicking the **sign up** 
        link below the Login button.
      * Once you have a user account, sign in with your username and password.

## Submit an experiment

1. Navigate to http://notyeti-191.lifemapper.org/boom/

1. In the left-hand pane, find and click on “New BOOM Project”

1. Select the occurrence data you want to use for this experiment.  
   These can be existing occurrence sets already on the server or 
   they can come from uploaded data.  In this example, we will 
   select existing data.

1. In the search text field under “Choose Occurrence Sets” type the 
   first few letters of the species you want to add to this 
   experiment.  Select the species name from the list.
   
1. You can repeat the choose occurrence set process as many times as 
   you want to build your experiment.  Each species will appear in 
   the list under “Choose Occurrence Sets”.  

1. There will be two icons at the right side of each species.  
   Clicking the trash can icon will remove the species from your 
   experiment.  The second icon is an “eye” and indicates which 
   species is shown in the map to the right of the species list.  An 
   eye icon with a line indicates that the species is hidden.

1. Once you have selected the species you want to include in the 
   experiment, select “SDM ALGORITHMS” from the banner above the map.

1. You can now add one or more modeling algorithms to use for your 
   experiment.  Simply hover over the “Add Algorithm” box and select 
   the name of the algorithm you want to include.

1. You can hover over a selected algorithm to see the parameters that 
   algorithm uses.  The algorithm will be configured with default 
   values for each of the parameters initially, but you can change the 
   values of those parameters as you see fit. 

1. You can add more algorithms if you would like by using the same
   procedure as step 8.

1. Once you have added all of the algorithms you want to use, select 
   “SDM LAYERS” from the top banner.

1. You will be presented with the available scenario packages that you 
   can use for your experiment. 

1. You can select one model scenario, indicated by a circle.  This model 
   scenario will be used with each of the SDMs created to create the 
   habitat suitability rule set.

1. You can then select any of the available projection scenarios for the 
   scenario package.  These are selected by clicking the square check 
   boxes.  In this example, there is only one projection scenario.

1. If you have a phylogenetic tree, you can click on the “TREE UPLOAD” 
   label in the banner to use the tree upload interface.  Your tree 
   should match the species you selected or uploaded. 

1. If you have biogeographic hypotheses, you can click on the “HYPOTHESES” 
   label in the banner and use the biogeographic hypotheses upload 
   interface.  Your hypotheses should be polygon shapefiles with one or two 
   features representing something like east and west of the Mississippi 
   river.

1. If you have phylogenetic data or biogeographic hypotheses, let us know 
   and we would be happy to help you use these services.

1. Finally, click “SUBMIT PROJECT” from the banner.

1. A check list will appear indicating what steps have been completed and 
   which are not.  The tree and Biogeographic Hypotheses steps are optional.

1. You can select to “Compete PAM stats” to generate macroecological 
   statistics using the Presence Absence Matrix (PAM) generated from your 
   selections.  Note that this makes the most sense when using multiple, 
   related, species that you wish to find larger scale patterns for.

1. Finally, give your experiment a name by filling in the “Job name” text 
   field and click the “SUBMIT JOB” button.

1. Your experiment is now submitted and will be inserted into the job 
   queue for computation.



