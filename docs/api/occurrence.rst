============================
SDM Occurrences REST Service
============================

.. contents::  

The Lifemapper SDM Occurrence REST service allows a user to count, list, post, 
get, and delete occurrence data layers used to create Species Distribution 
Modeling experiments in Lifemapper.

*********************
Count Occurrence Sets
*********************
Requests sent to the occurrence set count service will return the number of 
SDM occurrence sets that match the specified criteria for the specified user.

HTTP Method
===========
GET

URL
===
/api/v2/occurrence/count/{format}

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

+-----------------------+--------------------+------------+----------------------------------------------------------------------+
| Name                  | Type               | Example    | Description                                                          |
+=======================+====================+============+======================================================================+
| afterTime             | ISO 8601 Date time | 2015-05-13 | Count occurrence sets modified after this time                       |
+-----------------------+--------------------+------------+----------------------------------------------------------------------+
| beforeTime            | ISO 8601 Date time | 2014-12-03 | Count occurrence sets modified before this time                      |
+-----------------------+--------------------+------------+----------------------------------------------------------------------+
| displayName           | String             | Acer       | Count occurrence sets that have display names like this              |
+-----------------------+--------------------+------------+----------------------------------------------------------------------+
| epsgCode              | Integer            | 4326       | Count occurrence sets built using this EPSG code                     |
+-----------------------+--------------------+------------+----------------------------------------------------------------------+
| hasProjections        | Integer            | 1          | Count occurrence sets that have projections if this is set to 1      |
+-----------------------+--------------------+------------+----------------------------------------------------------------------+
| minimumNumberOfPoints | Integer            | 50         | Count occurrence sets that have at least this many points            |
+-----------------------+--------------------+------------+----------------------------------------------------------------------+
| public                | Integer            | 1          | (Only if logged in) Count public occurrence sets if this is set to 1 |
+-----------------------+--------------------+------------+----------------------------------------------------------------------+
   
Example
=======
For this example, we will count all of the occurrence sets with more than 100 points and request an XML document

Request::

      $ curl "http://svc.lifemapper.org/services/sdm/occurrences/count/xml?minimumNumberOfPoints=100"

Response::
   
   <?xml version="1.0" encoding="utf-8"?>
      <lm:response xmlns:lm="http://lifemapper.org" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://lifemapper.org /schemas/serviceResponse.xsd">
         <lm:title>Lifemapper List Service</lm:title>
         <lm:user>kubi</lm:user>
         <lm:items>
            <lm:denominator>1</lm:denominator>
            <lm:imag>0</lm:imag>
            <lm:numerator>51989</lm:numerator>
            <lm:real>51989</lm:real>
         </lm:items>
      </lm:response>

-----

*********************
Delete Occurrence Set
*********************
The delete occurrence set service removes an occurrence set you own from the Lifemapper system.

HTTP Method
===========
DELETE

URL
===
/services/sdm/occurrences/{occurrence set id}

Example
=======
For this example, we will delete occurrence set 99

Request::

      $ curl -X DELETE "http://svc.lifemapper.org/services/sdm/occurrences/99"

-----

******************
Get Occurrence Set
******************
The get occurrence set method retrieves an occurrence set that you own or that is public.

HTTP Method
===========
GET

URL
===
/services/sdm/occurrences/{occurrence set id}/{format}

Format Options
==============
+-----------+--------------------------------------+-----------------------------------------------------------+
| Format    | Content-Type                         | Description                                               |
+===========+======================================+===========================================================+
| (blank)   | text/html                            | Returns an HTML page containing occurrence set metadata   |
+-----------+--------------------------------------+-----------------------------------------------------------+
| atom      | application/atom+xml                 | Returns an atom feed for the occurrence set               |
+-----------+--------------------------------------+-----------------------------------------------------------+
| csv       | text/plain                           | Returns a CSV file of occurrence points                   |
+-----------+--------------------------------------+-----------------------------------------------------------+
| eml       | application/xml                      | Returns an EML document with occurrence set metadata      |
+-----------+--------------------------------------+-----------------------------------------------------------+
| html      | text/html                            | Returns an HTML page containing occurrence set metadata   |
+-----------+--------------------------------------+-----------------------------------------------------------+
| json      | application/json                     | Returns a JSON document with occurrence set metadata      |
+-----------+--------------------------------------+-----------------------------------------------------------+
| kml       | application/vnd.google-earth.kml+xml | Returns a KML document with points for the occurrence set |
+-----------+--------------------------------------+-----------------------------------------------------------+
| ogc       | ---                                  | OGC endpoint for making W\*S requests                     |
+-----------+--------------------------------------+-----------------------------------------------------------+
| shapefile | application/zip                      | Zipped shapefile of occurrence set data                   |
+-----------+--------------------------------------+-----------------------------------------------------------+
| xml       | application/xml                      | Returns an XML document with occurrence set metadata      |
+-----------+--------------------------------------+-----------------------------------------------------------+


Example
=======
For this example, we will get the shapefile for occurrence set 1000

Request::

      $ curl -X GET "http://svc.lifemapper.org/services/sdm/occurrences/1000/shapefile"

Response::

   Response is zip file with the files in the shapefile for the occurrence set

-----


********************
List Occurrence Sets
********************
The SDM occurrence sets listing services allows you to retrieve a list of Lifemapper occurrence sets that meet your specified criteria.  The "page" and "perPage" parameters provide a method to page through results since they are often too numerous to retrieve with one request

HTTP Method
===========
GET

URL
===
/services/sdm/occurrences/{format}

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
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| Name                  | Type               | Example    | Description                                                                        |
+=======================+====================+============+====================================================================================+
| afterTime             | ISO 8601 Date time | 2015-05-13 | Return occurrence sets modified after this time                                    |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| beforeTime            | ISO 8601 Date time | 2014-12-03 | Return occurrence sets modified before this time                                   |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| displayName           | String             | Acer       | Return occurrence sets that have display names like this                           |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| epsgCode              | Integer            | 4326       | Return occurrence sets built using this EPSG code                                  |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| fullObjects           | Integer            | 0          | If this is 1, return all object metadata, if it is 0, return small versions (less) |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| hasProjections        | Integer            | 1          | Return occurrence sets that have projections if this is set to 1                   |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| minimumNumberOfPoints | Integer            | 50         | Return occurrence sets that have at least this many points                         |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| page                  | Integer            | 3          | Return this page of results (zero-based count)                                     |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| perPage               | Integer            | 100        | Return this many results per page                                                  |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+
| public                | Integer            | 1          | (Only if logged in) Count public occurrence sets if this is set to 1               |
+-----------------------+--------------------+------------+------------------------------------------------------------------------------------+



Example
=======
In this example, we will request the 3rd page of results, with 2 results per page.  The occurrence sets should have at least 500 points and we'll request full objects in JSON.

Request::

      $ curl -X GET "http://svc.lifemapper.org/services/sdm/occurrences/json?page=3&perPage=2&minimumNumberOfPoints=500&fullObjects=1"

Response::

   {
      "title": "Lifemapper List Service",
      "items": 
      [
            {
               "SRS": "epsg:4326",
               "bbox": "(-113.31, 23.32, -89.87, 50.4)",
               "count": "500",
               "dataFormat": "ESRI Shapefile",
               "displayName": "Perdita albipennis",
               "epsgcode": "4326",
               "featureCount": "500",
               "feature": 
               [
               ],
               "fromGbif": "True",
               "id": "5831759",
               "isCategorical": "False",
               "keywords": 
               {
   
               },
               "layerName": "occ_5831759",
               "makeflowFilename": "/share/lmserver/data/archive/kubi/000/005/831/759/occ_5831759.mf",
               "mapFilename": "/share/lmserver/data/archive/kubi/000/005/831/759/data_5831759.map",
               "mapLayername": "occ_5831759",
               "mapName": "data_5831759",
               "mapPrefix": "http://yeti.lifemapper.org/ogc?map=data_5831759&layers=occ_5831759",
               "mapUnits": "",
               "maxX": "-89.87",
               "maxY": "50.4",
               "metadataUrl": "http://yeti.lifemapper.org/services/sdm/occurrences/5831759",
               "minX": "-113.31",
               "minY": "23.32",
               "modTime": "2016-08-12 08:01:28",
               "moduleType": "sdm",
               "name": "occ_5831759",
               "objId": "5831759",
               "ogrType": "1",
               "parametersModTime": "2016-08-12 08:01:28",
               "primaryEnv": "1",
               "queryCount": "500",
               "serviceType": "occurrences",
               "status": "300",
               "statusModTime": "2016-08-12 08:01:28",
               "title": "Perdita albipennis",
               "url": "http://yeti.lifemapper.org/services/sdm/occurrences/5831759",
               "user": "kubi",
               "verify": "9238b96e381ed6f068b0fafdab376c33eea2920ac013b22d3f25f5152bd0b784"
            },
            {
               "SRS": "epsg:4326",
               "bbox": "(-117.61, 32.92, -111.76, 37.18)",
               "count": "500",
               "dataFormat": "ESRI Shapefile",
               "displayName": "Perdita thermophila",
               "epsgcode": "4326",
               "featureCount": "500",
               "feature": 
               [
               ],
               "fromGbif": "True",
               "id": "5831749",
               "isCategorical": "False",
               "keywords": 
               {
               },
               "layerName": "occ_5831749",
               "makeflowFilename": "/share/lmserver/data/archive/kubi/000/005/831/749/occ_5831749.mf",
               "mapFilename": "/share/lmserver/data/archive/kubi/000/005/831/749/data_5831749.map",
               "mapLayername": "occ_5831749",
               "mapName": "data_5831749",
               "mapPrefix": "http://yeti.lifemapper.org/ogc?map=data_5831749&layers=occ_5831749",
               "mapUnits": "",
               "maxX": "-111.76",
               "maxY": "37.18",
               "metadataUrl": "http://yeti.lifemapper.org/services/sdm/occurrences/5831749",
               "minX": "-117.61",
               "minY": "32.92",
               "modTime": "2016-08-12 08:01:28",
               "moduleType": "sdm",
               "name": "occ_5831749",
               "objId": "5831749",
               "ogrType": "1",
               "parametersModTime": "2016-08-12 08:01:28",
               "primaryEnv": "1",
               "queryCount": "500",
               "serviceType": "occurrences",
               "status": "300",
               "statusModTime": "2016-08-12 08:01:28",
               "title": "Perdita thermophila",
               "url": "http://yeti.lifemapper.org/services/sdm/occurrences/5831749",
               "user": "kubi",
               "verify": "d96518c6f88be261a175cbf944ee61c20b5515fb491d1be0fdab811a013cd91d"
            }
      ],
      "itemCount": "18514",
      "userId": "kubi",
      "queryParameters": 
      {
         ...(omitted)...
      }
   }   
      
-----

*******************
Post Occurrence Set
*******************
The post occurrence set service allows you to post a new occurrence set for use in SDM experiments within Lifemapper

HTTP Method
===========
POST

URL
===
/services/sdm/occurrenes/{format}

Format Options
==============
The POST service supports the following interfaces for the response

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
Occurrence sets should be posted with metadata in the query parameters and the data in the content of the request

+-------------+---------+----------+-----------------------------------------------------------------------------------+
| Parameter   | Type    | Required | Description                                                                       |
+=============+=========+==========+===================================================================================+
| displayName | String  | Yes      | The display name for this occurrence set                                          |
+-------------+---------+----------+-----------------------------------------------------------------------------------+
| epsgCode    | Integer | Yes      | The EPSG code for the occurrence sets's map projection                            |
+-------------+---------+----------+-----------------------------------------------------------------------------------+
| name        | String  | No       | A short name for this occurrence set, note that this must be unique for each user |
+-------------+---------+----------+-----------------------------------------------------------------------------------+
| pointsType  | String  | Yes      | Either CSV or SHAPEFILE.  Indicates what the uploaded content is                  |
+-------------+---------+----------+-----------------------------------------------------------------------------------+

Example
=======
Post a new occurrence set named "My sample points", the data is in CSV format and EPSG:2163.  Occurrence data is in file points.csv.

Request::

   $ curl -X POST -H 'Content-type: text/csv' --data '@points.csv' http://svc.lifemapper.org/services/sdm/occurrences/?displayName=My%20sample%20points&pointsType=CSV&epsgCode=2163

Response::

  The response of this request is the same as if you ran a GET request on the occurrence set you just posted.  

-----

*********************
Occurrence Set Object
*********************

Sample JSON

.. code-block:: json

   {
      "title": "Aaptos suberitoides",
      "SRS": "epsg:4326",
      "bbox": "(55.3833, -8.32, 128.13333, 4.11833)",
      "count": "15",
      "dataFormat": "ESRI Shapefile",
      "displayName": "Aaptos suberitoides",
      "epsgcode": "4326",
      "featureCount": "15",
      "feature": 
      [
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_19868",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "11",
               "year": "2004",
               "coll_code": "Porifera",
               "geomwkt": "POINT (124.8433 1.38417)",
               "specieskey": "2251105",
               "day": "6",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "124.8433",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571939",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571939",
               "familykey": "8126",
               "dec_lat": "1.38417",
               "taxonkey": "2251105",
               "localid": "0",
               "rec_by": "Mike LeBlanc",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_16683",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "5",
               "year": "1997",
               "coll_code": "Porifera",
               "geomwkt": "POINT (119.3381 -5.1336)",
               "specieskey": "2251105",
               "day": "11",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "119.3381",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571919",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571919",
               "familykey": "8126",
               "dec_lat": "-5.1336",
               "taxonkey": "2251105",
               "localid": "1",
               "rec_by": "N.J. de Voogd",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_10721",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "12",
               "year": "1992",
               "coll_code": "Porifera",
               "geomwkt": "POINT (55.3833 -4.6333)",
               "specieskey": "2251105",
               "day": "9",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "55.3833",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571863",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571863",
               "familykey": "8126",
               "dec_lat": "-4.6333",
               "taxonkey": "2251105",
               "localid": "2",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_08192a",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "1",
               "year": "1984",
               "coll_code": "Porifera",
               "geomwkt": "POINT (128.13333 -3.75)",
               "specieskey": "2251105",
               "day": "1",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "128.13333",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571819",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571819",
               "familykey": "8126",
               "dec_lat": "-3.75",
               "taxonkey": "2251105",
               "localid": "3",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_10686",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "12",
               "year": "1992",
               "coll_code": "Porifera",
               "geomwkt": "POINT (55.4667 -4.5833)",
               "specieskey": "2251105",
               "day": "8",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "55.4667",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571860",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571860",
               "familykey": "8126",
               "dec_lat": "-4.5833",
               "taxonkey": "2251105",
               "localid": "4",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_11439",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "12",
               "year": "1992",
               "coll_code": "Porifera",
               "geomwkt": "POINT (55.7 -4.2833)",
               "specieskey": "2251105",
               "day": "17",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "55.7",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571871",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571871",
               "familykey": "8126",
               "dec_lat": "-4.2833",
               "taxonkey": "2251105",
               "localid": "5",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_13102",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "4",
               "year": "1997",
               "coll_code": "Porifera",
               "geomwkt": "POINT (119.342 -5.125)",
               "specieskey": "2251105",
               "day": "18",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "119.342",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571888",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571888",
               "familykey": "8126",
               "dec_lat": "-5.125",
               "taxonkey": "2251105",
               "localid": "6",
               "rec_by": "N.J. de Voogd",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_13204",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "4",
               "year": "1997",
               "coll_code": "Porifera",
               "geomwkt": "POINT (119.286 -5.102)",
               "specieskey": "2251105",
               "day": "13",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "119.286",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571891",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571891",
               "familykey": "8126",
               "dec_lat": "-5.102",
               "taxonkey": "2251105",
               "localid": "7",
               "rec_by": "N.J. de Voogd",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_08066",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "9",
               "year": "1984",
               "coll_code": "Porifera",
               "geomwkt": "POINT (118.24 -8.32)",
               "specieskey": "2251105",
               "day": "22",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "118.24",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571817",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571817",
               "familykey": "8126",
               "dec_lat": "-8.32",
               "taxonkey": "2251105",
               "localid": "8",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_08713",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "9",
               "year": "1984",
               "coll_code": "Porifera",
               "geomwkt": "POINT (123.975 -5.93333)",
               "specieskey": "2251105",
               "day": "11",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "123.975",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571829",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571829",
               "familykey": "8126",
               "dec_lat": "-5.93333",
               "taxonkey": "2251105",
               "localid": "9",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_11177",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "12",
               "year": "1992",
               "coll_code": "Porifera",
               "geomwkt": "POINT (55.5167 -4.7333)",
               "specieskey": "2251105",
               "day": "24",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "55.5167",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571870",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571870",
               "familykey": "8126",
               "dec_lat": "-4.7333",
               "taxonkey": "2251105",
               "localid": "10",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_10627",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "12",
               "year": "1992",
               "coll_code": "Porifera",
               "geomwkt": "POINT (55.8333 -4.3833)",
               "specieskey": "2251105",
               "day": "23",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "55.8333",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571859",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571859",
               "familykey": "8126",
               "dec_lat": "-4.3833",
               "taxonkey": "2251105",
               "localid": "11",
               "rec_by": "R.W.M. van Soest",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_13005",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "10",
               "year": "1996",
               "coll_code": "Porifera",
               "geomwkt": "POINT (119.3247 -5.0405)",
               "specieskey": "2251105",
               "day": "15",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "119.3247",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571887",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571887",
               "familykey": "8126",
               "dec_lat": "-5.0405",
               "taxonkey": "2251105",
               "localid": "12",
               "rec_by": "M. LeBlanc",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "ef6ac4b0-c063-11dd-a310-b8a03c50a862",
               "catnum": "POR_09630",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "ZMA",
               "month": "10",
               "year": "1980",
               "coll_code": "Porifera",
               "geomwkt": "POINT (119.3333 -4.9116)",
               "specieskey": "2251105",
               "day": "19",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "119.3333",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/351571842",
               "occurid": "0",
               "classkey": "199",
               "gbifid": "351571842",
               "familykey": "8126",
               "dec_lat": "-4.9116",
               "taxonkey": "2251105",
               "localid": "13",
               "rec_by": "H. Moll",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Naturalis Biodiversity Center"
            },
            {
               "datasetkey": "793c3890-6c8a-11de-8226-b8a03c50a862",
               "catnum": "Z004735",
               "basisofrec": "PRESERVED_SPECIMEN",
               "inst_code": "MAGNT",
               "month": "1",
               "year": "2004",
               "coll_code": "Sponge",
               "geomwkt": "POINT (118.62833 4.11833)",
               "specieskey": "2251105",
               "day": "27",
               "genuskey": "2243941",
               "sciname": "Aaptos suberitoides (Brndsted, 1934)",
               "dec_long": "118.62833",
               "phylumkey": "105",
               "gbifurl": "http://www.gbif.org/occurrence/1085961697",
               "occurid": "10",
               "classkey": "199",
               "gbifid": "1085961697",
               "familykey": "8126",
               "dec_lat": "4.11833",
               "taxonkey": "2251105",
               "localid": "14",
               "kingdomkey": "1",
               "orderkey": "1010",
               "puborgkey": "Museum and Art Gallery of the Northern Territory",
               "rec_by": 
               {
               }
            }
      ],
      "fromGbif": "True",
      "id": "5901017",
      "isCategorical": "False",
      "keywords": 
      {
      },
      "layerName": "occ_5901017",
      "makeflowFilename": "/share/lmserver/data/archive/kubi/000/005/901/017/occ_5901017.mf",
      "mapFilename": "/share/lmserver/data/archive/kubi/000/005/901/017/data_5901017.map",
      "mapLayername": "occ_5901017",
      "mapName": "data_5901017",
      "mapPrefix": "http://yeti.lifemapper.org/ogc?map=data_5901017&layers=occ_5901017",
      "mapUnits": "",
      "maxX": "128.13333",
      "maxY": "4.11833",
      "metadataUrl": "http://yeti.lifemapper.org/services/sdm/occurrences/5901017",
      "minX": "55.3833",
      "minY": "-8.32",
      "modTime": "2016-03-17 08:42:23",
      "moduleType": "sdm",
      "name": "occ_5901017",
      "objId": "5901017",
      "ogrType": "1",
      "parametersModTime": "2016-03-17 08:42:23",
      "primaryEnv": "1",
      "queryCount": "15",
      "serviceType": "occurrences",
      "status": "300",
      "statusModTime": "2016-03-17 08:42:23",
      "title": "Aaptos suberitoides",
      "user": "kubi",
      "verify": "fd610e552da89b18d1ce8595fcac6f7b8919e18119ce078861d373dd2ffb6c19"
   }
