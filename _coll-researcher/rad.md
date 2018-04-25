---
title: Multi-species (RAD) Analyses
image_path: ""
layout: page
---

## Lifemapper Multi-Species Range and Diveristy (RAD)

<p>
Studying biodiversity patterns includes describing, visualizing and analyzing 
different aspects of the numbers and abundances of taxa in both time and space. 
This can be done at multiple scales, looking at different resolutions of time, 
space, and even different levels of organism classification, like phylogenetic 
or taxonomic attributes.  Biodiversity patterns can be explained by species 
distributions and abundance.  These patterns are critical information for 
conservation and land management decisions.

There are major challenges related to study biodiversity patterns at large 
extents, high resolutions, and with thousands of species.  Lifemapper addresses 
these challenges by providing web services for assembling and analyzing many 
species distribution layers at multiple resolutions over arbitrary geographical 
extents.   These web services can be accessed programmatically and through the 
Lifemapper web app in the future.
</p>

## RAD Statistics


### Site-based statistics (for species)
* Alpha (species richness)
  - The number of species present at each site
* Alpha Prop (proportional species richness)
  - The proportion of the entire set of species that are present at each site.  Percentage of species pool 
    present.
* Phi (total range size)
  - The sum of the range sizes of all species at each site.
* Phi Prop (proportional species range size)
  - The proportion of the sum of the range sizes of all species at a site compared to the sum of all ranges 
    for all species.

### Site-based statistics (for tree)
* Mean Nearest Taxon Distance (for each species in this site, how taxonomically 
  close is its closest relative in this site)
* Mean Pairwise Distance (for each species in this site, how taxonomically 
  close are all other species in this site)
* Pearson’s correlation coefficient

### Species statistics
* Omega (range size)
* Omega Prop (range size in proportion to the total of all range sizes)
* PSI (the richness of a species’ range)
* PSI Prop (species range richness in proportion to richness all species ranges)

### Beta diversity statistics
* Whittakers Beta
* Landes Additive Beta
* Legendres Beta

### Covariance Matrices
* Sites composition
* Species ranges

### Schluter’s statistics
* Species variance ratio
* Sites variance ratio
