============================
SDM Projections REST Service
============================

.. contents::  

The Lifemapper SDM Projections REST service allows a user to count, list, post, get, and delete SDM projections

*****************
Count Projections
*****************
Requests sent to the projections count service will return the number of SDM projections that match the specified criteria for the specified user.

HTTP Method
===========
GET

URL
===
/services/sdm/projections/count/{format}

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

   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | Name            | Type               | Example    | Description                                                              |
   +=================+====================+============+==========================================================================+
   | afterTime       | ISO 8601 Date time | 2015-05-13 | Count projections modified after this time                               |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | algorithmCode   | String             | GARP_BS    | Count projections that used this algorithm to generate their model       |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | beforeTime      | ISO 8601 Date time | 2014-12-03 | Count projections modified before this time                              |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | displayName     | String             | Acacia     | Count projections that have occurrence sets with this display name       |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | epsgCode        | Integer            | 4326       | Count projections built using this EPSG code                             |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | experimentId    | Integer            | 88         | Count projections in this experiment                                     |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | occurrenceSetId | Integer            | 1234       | Count projections built with models built with this occurrence set       |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | scenarioId      | Integer            | 32         | Count projections that are in the scenario specified by this scenario id |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | status          | Integer            | 300        | Count projections that have this status (300 = Complete)                 |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+
   | public          | Integer            | 1          | (Only if logged in) Count public projections if this is set to 1         |
   +-----------------+--------------------+------------+--------------------------------------------------------------------------+

Example
=======
   For this example, we will count all of the projections that are in experiment 123 and request a JSON document as the response.

   Request
      $ curl "http://svc.lifemapper.org/services/sdm/projections/count/json?experimentId=123"

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

*****************
Delete Projection
*****************
   The delete projection service removes a projection you own from the Lifemapper system.

HTTP Method
===========
   DELETE

URL
===
   /services/sdm/projections/{projection id}

Example
=======
   For this example, we will delete projection 1234

   Request
      $ curl -X DELETE "http://svc.lifemapper.org/services/sdm/projections/1234"

-----

**************
Get Projection
**************
   The get projection method retrieves a projection that you own or that is public.

HTTP Method
===========
   GET

URL
===
   /services/sdm/projections/{projection id}/{format}

Format Options
==============
    +---------+--------------------------------------+----------------------------------------------------------------+
    | Format  | Content-Type                         | Description                                                    |
    +=========+======================================+================================================================+
    | (blank) | text/html                            | Returns an HTML page containing projection metadata            |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | AAIGrid | image/x-aaigrid                      | Returns an ASCII grid with projection data                     |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | atom    | application/atom+xml                 | Returns an atom feed for the projection                        |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | eml     | application/xml                      | Returns an EML document with projection metadata               |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | GTiff   | image/tiff                           | Returns a GeoTiff with projection data                         |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | html    | text/html                            | Returns an HTML page containing projection metadata            |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | json    | application/json                     | Returns a JSON document with projection metadata               |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | kml     | application/vnd.google-earth.kml+xml | Returns a KML document with a map image of the projection      |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | ogc     | ---                                  | OGC endpoint for making W\*S requests                          |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | package | application/zip                      | Returns a zipped package of outputs from the modeling software |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | status  | ---                                  | Can be given a format to return the status of a projection     |
    +---------+--------------------------------------+----------------------------------------------------------------+
    | xml     | application/xml                      | Returns an XML document with projection metadata               |
    +---------+--------------------------------------+----------------------------------------------------------------+


Example
=======
   For this example, we will get a kml document for projection 123

   Request
      $ curl -X GET "http://svc.lifemapper.org/services/sdm/projections/123/kml"

   Response
      Response is a KML document that will display the projection

-----


****************
List Projections
****************
   The SDM projections listing service allows you to retrieve a list of Lifemapper projections that meet your specified criteria.  The "page" and "perPage" parameters provide a method to page through results since they are often too numerous to retrieve with one request

HTTP Method
===========
   GET

URL
===
   /services/sdm/projections/{format}

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
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | Name            | Type               | Example    | Description                                                                        |
   +=================+====================+============+====================================================================================+
   | afterTime       | ISO 8601 Date time | 2015-05-13 | Return projections modified after this time                                        |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | algorithmCode   | String             | GARP_BS    | Return projections that used this algorithm to generate their model                |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | beforeTime      | ISO 8601 Date time | 2014-12-03 | Return projections modified before this time                                       |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | displayName     | String             | Acacia     | Return projections that have occurrence sets with this display name                |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | epsgCode        | Integer            | 4326       | Return projections built using this EPSG code                                      |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | experimentId    | Integer            | 88         | Return projections in this experiment                                              |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | fullObjects     | Integer            | 0          | If this is 1, return all object metadata, if it is 0, return small versions (less) |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | occurrenceSetId | Integer            | 1234       | Return projections built with models built with this occurrence set                |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | page            | Integer            | 3          | Return this page of results (zero-based count)                                     |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | perPage         | Integer            | 100        | Return this many results per page                                                  |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | scenarioId      | Integer            | 32         | Return projections that are in the scenario specified by this scenario id          |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | status          | Integer            | 300        | Return projections that have this status (300 = Complete)                          |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+
   | public          | Integer            | 1          | (Only if logged in) Return public projections if this is set to 1                  |
   +-----------------+--------------------+------------+------------------------------------------------------------------------------------+




Example
=======
   In this example, we will request the 100th page of results with 2 results per page for completed projections and get the response as JSON

   Request
      $ curl -X GET "http://svc.lifemapper.org/services/sdm/projections/json?perPage=2&page=100&status=300"

   Response

      .. code-block:: json

         {
            "title": "Lifemapper List Service",
            "items": 
            [
                  {
                     "epsgcode": "4326",
                     "id": "6707802",
                     "modTime": "2016-08-14 15:02:48",
                     "title": "Perdita covilleae",
                     "url": "http://yeti.lifemapper.org/services/sdm/projections/6707802"
                  },
                  {
                     "epsgcode": "4326",
                     "id": "6707804",
                     "modTime": "2016-08-14 15:02:48",
                     "title": "Perdita covilleae",
                     "url": "http://yeti.lifemapper.org/services/sdm/projections/6707804"
                  }
            ],
            "itemCount": "1290131",
            "userId": "kubi",
            "queryParameters": 
            {
               "status": 
               {
                  "value": "300",
                  "param": 
                  {
                     "displayName": "Projection Status",
                     "name": "status",
                     "multiplicity": "1",
                     "documentation": "",
                     "type": "integer",
                     "options": 
                     {
                        "options": 
                        [
                              {
                                 "name": "Initialized",
                                 "value": "1"
                              },
                              {
                                 "name": "Completed",
                                 "value": "300"
                              },
                              {
                                 "name": "Obsolete",
                                 "value": "60"
                              }
                        ]
                     }
                  }
               },
               ... (omitted) ...
            }
         }         

-----

*****************
Projection Object
*****************

   Sample JSON

      .. code-block:: json

         {
            "title": "Perdita covilleae Projection 6707804",
            "SRS": "epsg:4326",
            "algorithmCode": "BIOCLIM",
            "bbox": "(-180.0, -60.0, 180.0, 90.0)",
            "createTime": "2015-11-21 01:39:35",
            "dataFormat": "GTiff",
            "description": "Predicted habitat for Perdita covilleae projected onto CCSM4-mid-10min datalayers",
            "epsgcode": "4326",
            "gdalType": "1",
            "geoTransform": 
            {
               "geoTransform": "-180.0",
               "geoTransform": "0.166666666667",
               "geoTransform": "0.0",
               "geoTransform": "90.0",
               "geoTransform": "0.0",
               "geoTransform": "-0.166666666667"
            },
            "id": "6707804",
            "isCategorical": "False",
            "keywords": 
            {
               "keyword": "bioclimatic variables",
               "keyword": "climate",
               "keyword": "elevation",
               "keyword": "habitat model",
               "keyword": "BIOCLIM",
               "keyword": "past",
               "keyword": "Perdita covilleae",
               "keyword": "predicted"
            },
            "layers": 
            {
               "layers": 
               [
                  {
                     "SRS": "epsg:4326",
                     "bbox": "(-180.0, -60.0, 180.0, 90.0)",
                     "dataFormat": "GTiff",
                     "description": "Mean Temperature of Warmest Quarter, Predicted mid holocene (~ 6000 years ago) climate calculated from change modeled by Community Climate System Model, 4.0, National Center for Atmospheric Research (NCAR) http://www.cesm.ucar.edu/models/ccsm4.0/ for Coupled Model Intercomparison Project Phase 5 plus Worldclim 1.4 observed mean climate",
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
                     "id": "7419",
                     "isCategorical": "False",
                     "keywords": 
                     {
                        "keyword": "warmest quarter",
                        "keyword": "temperature",
                        "keyword": "mean"
                     },
                     "mapLayername": "ccmidbi10-10min",
                     "mapPrefix": "http://yeti.lifemapper.org/ogc?map=usr_kubi_4326&layers=ccmidbi10-10min",
                     "mapUnits": "dd",
                     "maxVal": "382.0",
                     "maxX": "180.0",
                     "maxY": "90.0",
                     "metadataUrl": "http://yeti.lifemapper.org/services/sdm/layers/7419",
                     "minVal": "-90.0",
                     "minX": "-180.0",
                     "minY": "-60.0",
                     "modTime": "2015-11-19 16:08:10",
                     "moduleType": "sdm",
                     "name": "ccmidbi10-10min",
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
                     "title": "Mean Temperature of Warmest Quarter, Mid Holocene (~ 6000 years ago), 10min",
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
                     "verify": "e53a0e86cbed1199f6f200d865e83de51099e6e35705e56af40884aa8dfc13e7"
                  },
                  ... (more layers omitted) ...
               ]
            },
            "makeflowFilename": "/share/lmserver/data/archive/kubi/000/005/831/827/occ_5831827.mf",
            "mapFilename": "/share/lmserver/data/archive/kubi/000/005/831/827/data_5831827.map",
            "mapLayername": "prj_6707804",
            "mapName": "data_5831827",
            "mapPrefix": "http://yeti.lifemapper.org/ogc?map=data_5831827&layers=prj_6707804",
            "mapUnits": "dd",
            "maxVal": "50.0",
            "maxX": "180.0",
            "maxY": "90.0",
            "metadataUrl": "http://yeti.lifemapper.org/services/sdm/projections/6707804",
            "minVal": "0.0",
            "minX": "-180.0",
            "minY": "-60.0",
            "modTime": "2016-08-14 15:02:48",
            "moduleType": "sdm",
            "name": "prj_6707804",
            "nodataVal": "127.0",
            "objId": "6707804",
            "parametersModTime": "2016-08-14 15:02:48",
            "priority": "1",
            "resolution": "0.16667",
            "scenarioCode": "CCSM4-mid-10min",
            "serviceType": "projections",
            "size": 
            {
               "size": "2160",
               "size": "900"
            },
            "speciesName": "Perdita covilleae",
            "srs": "GEOGCS['WGS 84',DATUM['WGS_1984',SPHEROID['WGS 84',6378137,298.257223563,AUTHORITY['EPSG','7030']],AUTHORITY['EPSG','6326']],PRIMEM['Greenwich',0],UNIT['degree',0.0174532925199433],AUTHORITY['EPSG','4326']]",
            "status": "300",
            "statusModTime": "2016-08-14 15:02:48",
            "title": "Perdita covilleae Projection 6707804",
            "user": "kubi",
            "verify": "3426e51a28bed25f656b2beb601249892e66b159a2482f2be168c066f954b297"
         }
         
