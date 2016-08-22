==========================
SDM Scenarios REST Service
==========================

.. contents::  

The Lifemapper SDM Scenarios REST service allows a user to count, list, post, get, and delete environmental scenarios used to create Species Distribution Modeling experiments in Lifemapper.

***************
Count Scenarios
***************
Requests sent to the scenario count service will return the number of SDM scenarios that match the specified criteria for the specified user.

HTTP Method
===========
GET

URL
===
/services/sdm/scenarios/count/{format}

Format Options
==============

+---------+------------------+
| Format  | Content-Type     |
+=========+==================+
| (blank) | application/xml  |
+---------+------------------+
| XML     | application/xml  |
+---------+------------------+
| JSON    | application/json |
+---------+------------------+

Query Parameters
================

   +------------------+--------------------+------------+----------------------------------------------------------------+
   | Name             | Type               | Example    | Description                                                    |
   +==================+====================+============+================================================================+
   | afterTime        | ISO 8601 Date time | 2015-05-13 | Count scenarios modified after this time                       |
   +------------------+--------------------+------------+----------------------------------------------------------------+
   | beforeTime       | ISO 8601 Date time | 2014-12-03 | Count scenarios modified before this time                      |
   +------------------+--------------------+------------+----------------------------------------------------------------+
   | epsgCode         | Integer            | 4326       | Count scenarios built using this EPSG code                     |
   +------------------+--------------------+------------+----------------------------------------------------------------+
   | keyword          | String             | observed   | Count scenarios that have this keyword (can have multiple)     |
   +------------------+--------------------+------------+----------------------------------------------------------------+
   | matchingScenario | Integer            | 32         | Count scenarios that match the scenario specified by this id   |
   +------------------+--------------------+------------+----------------------------------------------------------------+
   | public           | Integer            | 1          | (Only if logged in) Count public scenarios if this is set to 1 |
   +------------------+--------------------+------------+----------------------------------------------------------------+

Example
=======
   For this example, we will count all of the scenarios that match scenario 34 and request a JSON document as the response.

   Request
      $ curl "http://svc.lifemapper.org/services/sdm/scenarios/count/json?matchingScenario=34"

   Response
   
      .. code-block:: json

         {
            "title": "Lifemapper List Service",
            "denominator": "1",
            "imag": "0",
            "numerator": "4",
            "real": "4"
         }

-----

***************
Delete Scenario
***************
   The delete scenario service removes a scenario you own from the Lifemapper system.  

HTTP Method
===========
   DELETE

URL
===
   /services/sdm/scenarios/{scenario id}

Example
=======
   For this example, we will delete scenario 1

   Request
      $ curl -X DELETE "http://svc.lifemapper.org/services/sdm/scenarios/1"

-----

***********
Get Scenrio
***********
   The get scenario method retrieves a scenario that you own or that is public.

HTTP Method
===========
   GET

URL
===
   /services/sdm/scenario/{scenario id}/{format}

Format Options
==============
    +---------+--------------------------------------+---------------------------------------------------+
    | Format  | Content-Type                         | Description                                       |
    +=========+======================================+===================================================+
    | (blank) | text/html                            | Returns an HTML page containing scenario metadata |
    +---------+--------------------------------------+---------------------------------------------------+
    | atom    | application/atom+xml                 | Returns an atom feed for the scenario             |
    +---------+--------------------------------------+---------------------------------------------------+
    | eml     | application/xml                      | Returns an EML document with scenario metadata    |
    +---------+--------------------------------------+---------------------------------------------------+
    | html    | text/html                            | Returns an HTML page containing scenario metadata |
    +---------+--------------------------------------+---------------------------------------------------+
    | json    | application/json                     | Returns a JSON document with scenario metadata    |
    +---------+--------------------------------------+---------------------------------------------------+
    | xml     | application/xml                      | Returns an XML document with scenario metadata    |
    +---------+--------------------------------------+---------------------------------------------------+


Example
=======
   For this example, we will get the metadata for scenario 2 in eml format
   
   Request
      $ curl -X GET "http://svc.lifemapper.org/services/sdm/scenarios/2/eml"

   Response
      Response is scenario EML document

-----


**************
List Scenarios
**************
   The SDM scenarios listing services allows you to retrieve a list of Lifemapper scenarios that meet your specified criteria.  The "page" and "perPage" parameters provide a method to page through results since they are often too numerous to retrieve with one request

HTTP Method
===========
   GET

URL
===
   /services/sdm/scenarios/{format}

Format Options
==============
    +---------+----------------------+
    | Format  | Content-Type         |
    +=========+======================+
    | (blank) | text/html            |
    +---------+----------------------+
    | ATOM    | application/atom+xml |
    +---------+----------------------+
    | HTML    | text/html            |
    +---------+----------------------+
    | JSON    | application/json     |
    +---------+----------------------+
    | XML     | application/xml      |
    +---------+----------------------+


Query Parameters
================
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | Name             | Type               | Example    | Description                                                                        |
   +==================+====================+============+====================================================================================+
   | afterTime        | ISO 8601 Date time | 2015-05-13 | Return scenarios modified after this time                                          |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | beforeTime       | ISO 8601 Date time | 2014-12-03 | Return scenarios modified before this time                                         |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | epsgCode         | Integer            | 4326       | Return scenarios built using this EPSG code                                        |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | fullObjects      | Integer            | 0          | If this is 1, return all object metadata, if it is 0, return small versions (less) |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | keyword          | String             | observed   | Return scenarios that have this keyword (can have multiple)                        |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | matchingScenario | Integer            | 32         | Return scenarios that match the scenario specified by this id                      |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | page             | Integer            | 3          | Return this page of results (zero-based count)                                     |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | perPage          | Integer            | 100        | Return this many results per page                                                  |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+
   | public           | Integer            | 1          | (Only if logged in) Return public scenarios if this is set to 1                    |
   +------------------+--------------------+------------+------------------------------------------------------------------------------------+



Example
=======
   In this example, we will request the 0th page of results with 3 results per page as an ATOM feed

   Request
      $ curl -X GET "http://svc.lifemapper.org/services/sdm/scenarios/atom?page=0&perPage=3"

   Response

      .. code-block:: xml

         <feed xmlns="http://www.w3.org/2005/Atom">
            <id>http://yeti.lifemapper.org/services/sdm/scenarios/atom</id>
            <title>Lifemapper List Service</title>
            <link href="http://yeti.lifemapper.org/services/sdm/scenarios/atom" rel="self" />
            <updated>2016-08-19T20:57:07Z</updated>
            <author>
               <name>Lifemapper</name>
               <email>no-reply-lifemapper@yeti.lifemapper.org</email>
            </author>
            <link href="http://yeti.lifemapper.org/services/sdm/scenarios/atom/?page=0&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;keyword=[]&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="first" />
            <link href="http://yeti.lifemapper.org/services/sdm/scenarios/atom/?page=0&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;keyword=[]&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="current" />
            <link href="http://yeti.lifemapper.org/services/sdm/scenarios/atom/?page=1&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;keyword=[]&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="next" />
            <link href="http://yeti.lifemapper.org/services/sdm/scenarios/atom/?page=2&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;keyword=[]&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="last" />
            <entry>
               <id>http://yeti.lifemapper.org/services/sdm/scenarios/1551</id>
               <link href="http://yeti.lifemapper.org/services/sdm/scenarios/1551/atom" rel="self" />
               <link href="http://yeti.lifemapper.org/services/sdm/scenarios/1551/atom" rel="alternate" />
               <title>CCSM4, IPCC AR5 RCP4.5, 2041-2060, 10min</title>
               <updated>2015-11-19T16:08:10Z</updated>
               <summary>CCSM4, IPCC AR5 RCP4.5, 2041-2060, 10min</summary>
            </entry>
            <entry>
               <id>http://yeti.lifemapper.org/services/sdm/scenarios/1550</id>
               <link href="http://yeti.lifemapper.org/services/sdm/scenarios/1550/atom" rel="self" />
               <link href="http://yeti.lifemapper.org/services/sdm/scenarios/1550/atom" rel="alternate" />
               <title>CCSM4, IPCC AR5 RCP8.5, 2041-2060, 10min</title>
               <updated>2015-11-19T16:08:10Z</updated>
               <summary>CCSM4, IPCC AR5 RCP8.5, 2041-2060, 10min</summary>
            </entry>
            <entry>
               <id>http://yeti.lifemapper.org/services/sdm/scenarios/1549</id>
               <link href="http://yeti.lifemapper.org/services/sdm/scenarios/1549/atom" rel="self" />
               <link href="http://yeti.lifemapper.org/services/sdm/scenarios/1549/atom" rel="alternate" />
               <title>CCSM4, IPCC AR5 RCP4.5, 2061-2080, 10min</title>
               <updated>2015-11-19T16:08:10Z</updated>
               <summary>CCSM4, IPCC AR5 RCP4.5, 2061-2080, 10min</summary>
            </entry>
         </feed>
         
-----

*************
Post Scenario
*************
   The post scenario service allows you to post a new environmental scenario for use in SDM experiments within Lifemapper

HTTP Method
===========
   POST

URL
===
   /services/sdm/scenarios/{format}

Format Options
==============
   The POST service supports the following interfaces for the response:
    +---------+----------------------+
    | Format  | Content-Type         |
    +=========+======================+
    | (blank) | text/html            |
    +---------+----------------------+
    | ATOM    | application/atom+xml |
    +---------+----------------------+
    | HTML    | text/html            |
    +---------+----------------------+
    | JSON    | application/json     |
    +---------+----------------------+
    | XML     | application/xml      |
    +---------+----------------------+

POST Query Parameters
=====================

   Scenarios can be posted using the query parameters below, or with an XML request following the schema at: http://lifemapper.org/schemas/serviceRequest.xsd.

   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Type     | Required | Description                                                                                                                                  |
   +=============+==========+==========+==============================================================================================================================================+
   | author      | String   | No       | The author of this scenario                                                                                                                  |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | code        | String   | Yes      | A short name for the scenario                                                                                                                |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | description | String   | No       | A longer description of the scenario                                                                                                         |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | endDate     | ISO 8601 | No       | The ending date for this scenario                                                                                                            |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | epsgCode    | Integer  | Yes      | The EPSG code for the scenario's map projection                                                                                              |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | keyword     | String   | No       | A keyword associated with the scenario (add more keyword parameters for multiple keywords ex. keyword=kw1&keyword=kw2)                       |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | layer       | Integer  | Yes      | An integer representing the id of a layer to add to the scenario, duplicate this parameter to add more layers ex. layer=1&layer=32&layer=322 | 
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | resolution  | Numeric  | No       | The resolution of the cell, in number of (cell) units per cell                                                                               |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | startDate   | ISO 8601 | No       | The start date for this scenario                                                                                                             |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | title       | String   | No       | A title for the scenario                                                                                                                     |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+
   | units       | String   | Yes      | The cell size units                                                                                                                          |
   +-------------+----------+----------+----------------------------------------------------------------------------------------------------------------------------------------------+


Example
=======
   Post a new scenario with the code: sample, epsg: 4326, layers: 1, 2, 3, 4, and units: dd

   Request
      .. code-block:: bash
      
         $ curl -X POST http://svc.lifemapper.org/services/sdm/scenarios/?code=sample&epsgCode=4326&layer=1&layer=2&layer=3&layer=4&units=dd

   Response
     The response of this request is the same as if you ran a GET request on the scenario you just posted.  

-----

***************
Scenario Object
***************

   Sample JSON

      .. code-block:: json

         {
            "title": "CCSM4, IPCC AR5 RCP4.5, 2061-2080, 10min",
            "SRS": "epsg:4326",
            "author": "National Center for Atmospheric Research (NCAR) http://www.cesm.ucar.edu/models/ccsm4.0/",
            "bbox": "(-180.0, -60.0, 180.0, 90.0)",
            "code": "CCSM4-RCP4.5-2070-10min",
            "count": "20",
            "description": "Predicted 2061-2080 climate calculated from change modeled by Community Climate System Model, 4.0, National Center for Atmospheric Research (NCAR) http://www.cesm.ucar.edu/models/ccsm4.0/ for the IPCC Fifth Assessment Report (2013), Scenario RCP4.5 plus Worldclim 1.4 observed mean climate",
            "endDate": "1864-07-28 00:00:00",
            "epsgcode": "4326",
            "id": "1549",
            "intersectBounds": 
            {
               "intersectBound": "-180.0",
               "intersectBound": "-60.0",
               "intersectBound": "180.0",
               "intersectBound": "90.0"
            },
            "intersectKeywords": 
            {
         
            },
            "keywords": 
            {
               "keyword": "climate",
               "keyword": "elevation",
               "keyword": "bioclimatic variables",
               "keyword": "future",
               "keyword": "predicted",
               "keyword": "radiative forcing +4.5",
               "keyword": "likely temperature increase 1.1-2.6 C"
            },
            "layers": 
            {
               "layers": 
               [
                  {
                     "SRS": "epsg:4326",
                     "bbox": "(-180.0, -60.0, 180.0, 90.0)",
                     "dataFormat": "GTiff",
                     "description": "Mean Temperature of Warmest Quarter, Predicted 2061-2080 climate calculated from change modeled by Community Climate System Model, 4.0, National Center for Atmospheric Research (NCAR) http://www.cesm.ucar.edu/models/ccsm4.0/ for the IPCC Fifth Assessment Report (2013), Scenario RCP4.5 plus Worldclim 1.4 observed mean climate",
                     "endDate": "1864-07-28 00:00:00",
                     "epsgcode": "4326",
                     "gdalType": "3",
                     "geoTransform": 
                     {
                        "geoTransform": "-180.0",
                        "geoTransform": "0.166666666667",
                        "geoTransform": "0.0",
                        "geoTransform": "90.0",
                        "geoTransform": "0.0",
                        "geoTransform": "-0.166666666667"
                     },
                     "id": "7457",
                     "isCategorical": "False",
                     "keywords": 
                     {
                        "keyword": "warmest quarter",
                        "keyword": "temperature",
                        "keyword": "mean"
                     },
                     "mapLayername": "cc45bi7010-10min",
                     "mapPrefix": "http://yeti.lifemapper.org/ogc?map=usr_kubi_4326&layers=cc45bi7010-10min",
                     "mapUnits": "dd",
                     "maxVal": "411.0",
                     "maxX": "180.0",
                     "maxY": "90.0",
                     "metadataUrl": "http://yeti.lifemapper.org/services/sdm/layers/7457",
                     "minVal": "-75.0",
                     "minX": "-180.0",
                     "minY": "-60.0",
                     "modTime": "2015-11-19 16:08:10",
                     "moduleType": "sdm",
                     "name": "cc45bi7010-10min",
                     "nodataVal": "-32768.0",
                     "parametersModTime": "2015-11-18 20:41:01",
                     "resolution": "0.16667",
                     "serviceType": "layers",
                     "size": 
                     {
                        "size": "2160",
                        "size": "900"
                     },
                     "srs": "GEOGCS['WGS 84',DATUM['unknown',SPHEROID['WGS84',6378137,298.257223563],TOWGS84[0,0,0,0,0,0,0]],PRIMEM['Greenwich',0],UNIT['degree',0.0174532925199433]]",
                     "startDate": "1864-07-09 00:00:00",
                     "title": "Mean Temperature of Warmest Quarter, IPCC AR5 RCP4.5, 2070, 10min",
                     "typeCode": "BIO10",
                     "typeDescription": "Mean Temperature of Warmest Quarter",
                     "typeKeywords": 
                     {
                        "typeKeyword": "warmest quarter",
                        "typeKeyword": "temperature",
                        "typeKeyword": "mean"
                     },
                     "typeTitle": "Mean Temperature of Warmest Quarter",
                     "user": "kubi",
                     "valUnits": "degreesCelsiusTimes10",
                     "verify": "8359c2b540175a6643f8220301d38554767a794429a21c0c8abd4a293f38f5a6"
                  },
                  ... (omitted layers) ...
               ]
            },
            "mapFilename": "/share/lmserver/data/archive/kubi/maps/scen_CCSM4-RCP4.5-2070-10min.map",
            "mapName": "scen_CCSM4-RCP4.5-2070-10min",
            "mapPrefix": "http://yeti.lifemapper.org/ogc?map=usr_kubi",
            "maxX": "180.0",
            "maxY": "90.0",
            "metadataUrl": "http://yeti.lifemapper.org/services/sdm/scenarios/1549",
            "minX": "-180.0",
            "minY": "-60.0",
            "modTime": "2015-11-19 16:08:10",
            "moduleType": "sdm",
            "name": "CCSM4-RCP4.5-2070-10min",
            "resolution": "0.16667",
            "serviceType": "scenarios",
            "startDate": "1864-07-09 00:00:00",
            "title": "CCSM4, IPCC AR5 RCP4.5, 2061-2080, 10min",
            "unionBounds": 
            {
               "unionBound": "-180.0",
               "unionBound": "-60.0",
               "unionBound": "180.0",
               "unionBound": "90.0"
            },
            "unionKeywords": 
            {
               "unionKeyword": "warmest quarter",
               "unionKeyword": "elevation",
               "unionKeyword": "coldest month",
               "unionKeyword": "seasonality",
               "unionKeyword": "isothermality",
               "unionKeyword": "coldest quarter",
               "unionKeyword": "wettest quarter",
               "unionKeyword": "precipitation",
               "unionKeyword": "temperature",
               "unionKeyword": "driest month",
               "unionKeyword": "warmest month",
               "unionKeyword": "annual",
               "unionKeyword": "wettest month",
               "unionKeyword": "driest quarter",
               "unionKeyword": "range",
               "unionKeyword": "min",
               "unionKeyword": "max",
               "unionKeyword": "mean"
            },
            "units": "dd",
            "user": "kubi"
         }
