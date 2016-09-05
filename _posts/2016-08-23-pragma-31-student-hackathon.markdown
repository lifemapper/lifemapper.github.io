---
layout: post
title:  "PRAGMA 31 Student Hackathon Task #3"
date:   2016-08-23 11:42:42 -0500
---


# Contents
{:.no_toc}

* Will be replaced with the ToC, excluding the "Contents" header
{:toc}

## Goal
The goal is to create a nice, dynamically updated webpage with visualizations 
of the Lifemapper Catalog contents, status, and speed of computation.  The 
page should be a tool for Lifemapper developers or administrators to diagnose
problems with the installation or data.  The 
visualization need not be published on a live site, but should query the live
KU Lifemapper services.

## Background
To get an overall understanding of the Lifemapper Software and the contents of 
the Catalog, read the [Overview](/overview.html) page.

## Documentation
All documentation is listed in the [Documentation](/documentation.html) page.

The two primary ways of accessing Lifemapper webservices are the 
[Python client library](/lmclient/description/), an easy wrapper for
Lifemapper services.  Example code is linked off this page. Doxygen 
documentation for the Python client library starts
[here](/docs/clientLibrary).  Dig into the 'Classes' for the 
[SDM Client functions](/docs/clientLibrary/classLmClient_1_1sdm_1_1SDMClient.html) 
and 
[RAD Client functions](/docs/clientLibrary/classLmClient_1_1rad_1_1RADClient.html)

If you prefer
to call the web services from another language, check out the 
[REST API](/api.html) documentation.  These pages allow you to construct and 
test raw URL queries, however, not all formats and constant enumerations 
are described on these pages.

