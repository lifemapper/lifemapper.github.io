=======================
SDM Layers REST Service
=======================

.. contents::  

The Lifemapper SDM Layers REST service allows a user to count, list, post, get, 
and delete environmental layers used to create Species Distribution Modeling 
experiments in Lifemapper.

************
Count Layers
************
Requests sent to the layer count service will return the number of SDM layers 
that match the specified criteria for the specified user.

HTTP Method
===========
GET

URL
===
/services/sdm/layers/count/{format}

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

+---------------+--------------------+------------+---------------------------------------------------------------------+
| Name          | Type               | Example    | Description                                                         |
+===============+====================+============+=====================================================================+
| afterTime     | ISO 8601 Date time | 2015-05-13 | Count layers modified after this time                               |
+---------------+--------------------+------------+---------------------------------------------------------------------+
| beforeTime    | ISO 8601 Date time | 2014-12-03 | Count layers modified before this time                              |
+---------------+--------------------+------------+---------------------------------------------------------------------+
| epsgCode      | Integer            | 4326       | Count layers built using this EPSG code                             |
+---------------+--------------------+------------+---------------------------------------------------------------------+
| isCategorical | Integer            | 1          | Count layers marked as categorical (1 yes, 0 no)                    |
+---------------+--------------------+------------+---------------------------------------------------------------------+
| scenarioId    | Integer            | 32         | Count layers that are in the scenario specified by this scenario id |
+---------------+--------------------+------------+---------------------------------------------------------------------+
| typeCode      | String             | rainfall   | Count layers that have this type code                               |
+---------------+--------------------+------------+---------------------------------------------------------------------+
| public        | Integer            | 1          | (Only if logged in) Count public layers if this is set to 1         |
+---------------+--------------------+------------+---------------------------------------------------------------------+

Example
=======
For this example, we will count all of the layers that are in the scenario 34 
and request a JSON document as the response.

Request::

   $ curl "http://svc.lifemapper.org/services/sdm/layers/count/json?scenario=34"

Response
   
.. code-block:: json

         {
            "title": "Lifemapper List Service",
            "denominator": "1",
            "imag": "0",
            "numerator": "19",
            "real": "19"
         }

-----

************
Delete Layer
************
The delete layer service removes a layer you own from the Lifemapper system.  
You may want to do this if you think a layer is invalid.

HTTP Method
===========
DELETE

URL
===
/services/sdm/layers/{layer id}

Example
=======
For this example, we will delete layer 4444

Request::

    $ curl -X DELETE "http://svc.lifemapper.org/services/sdm/layers/4444"

-----

*********
Get Layer
*********
The get layer method retrieves a layer that you own or that is public.

HTTP Method
===========
GET

URL
===
/services/sdm/layers/{layer id}/{format}

Format Options
==============
+---------+--------------------------------------+------------------------------------------------------+
| Format  | Content-Type                         | Description                                          |
+=========+======================================+======================================================+
| (blank) | text/html                            | Returns an HTML page containing layer metadata       |
+---------+--------------------------------------+------------------------------------------------------+
| AAIGrid | image/x-aaigrid                      | Returns an ASCII grid with layer data                |
+---------+--------------------------------------+------------------------------------------------------+
| atom    | application/atom+xml                 | Returns an atom feed for the layer                   |
+---------+--------------------------------------+------------------------------------------------------+
| eml     | application/xml                      | Returns an EML document with layer metadata          |
+---------+--------------------------------------+------------------------------------------------------+
| GTiff   | image/tiff                           | Returns a GeoTiff with layer data                    |
+---------+--------------------------------------+------------------------------------------------------+
| html    | text/html                            | Returns an HTML page containing layer metadata       |
+---------+--------------------------------------+------------------------------------------------------+
| json    | application/json                     | Returns a JSON document with layer metadata          |
+---------+--------------------------------------+------------------------------------------------------+
| kml     | application/vnd.google-earth.kml+xml | Returns a KML document with a map image of the layer |
+---------+--------------------------------------+------------------------------------------------------+
| ogc     | ---                                  | OGC endpoint for making W\*S requests                |
+---------+--------------------------------------+------------------------------------------------------+
| xml     | application/xml                      | Returns an XML document with layer metadata          |
+---------+--------------------------------------+------------------------------------------------------+


Example
=======
For this example, we will get the data for layer 123 in GeoTiff format

Request::

   $ curl -X GET "http://svc.lifemapper.org/services/sdm/layers/123/GTiff"

Response: 
   Response is binary geotiff data

-----


***********
List Layers
***********
The SDM layers listing services allows you to retrieve a list of Lifemapper 
layers that meet your specified criteria.  The "page" and "perPage" parameters 
provide a method to page through results since they are often too numerous to 
retrieve with one request

HTTP Method
===========
GET

URL
===
/services/sdm/layers/{format}

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
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| Name          | Type               | Example    | Description                                                                        |
+===============+====================+============+====================================================================================+
| afterTime     | ISO 8601 Date time | 2015-05-13 | Return layers modified after this time                                             |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| beforeTime    | ISO 8601 Date time | 2014-12-03 | Return layers modified before this time                                            |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| epsgCode      | Integer            | 4326       | Return layers built using this EPSG code                                           |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| fullObjects   | Integer            | 0          | If this is 1, return all object metadata, if it is 0, return small versions (less) |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| isCategorical | Integer            | 1          | Return layers marked as categorical (1 yes, 0 no)                                  |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| page          | Integer            | 3          | Return this page of results (zero-based count)                                     |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| perPage       | Integer            | 100        | Return this many results per page                                                  |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| scenarioId    | Integer            | 32         | Return layers that are in the scenario specified by this scenario id               |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| typeCode      | String             | rainfall   | Return layers that have this type code                                             |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+
| public        | Integer            | 1          | (Only if logged in) Return public layers if this is set to 1                       |
+---------------+--------------------+------------+------------------------------------------------------------------------------------+


Example
=======
In this example, we will request the 0th page of results with 2 results per page.  
The layers should have EPSG code 4326 and the response will be XML.

Request::

      $ curl -X GET "http://svc.lifemapper.org/services/sdm/layers/xml?page=0&perPage=2&epsgCode=4326"

Response

.. code-block:: xml

         <?xml version="1.0" encoding="utf-8"?>
         <lm:response xmlns:lm="http://lifemapper.org" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://lifemapper.org /schemas/serviceResponse.xsd">
            <lm:title>Lifemapper List Service</lm:title>
            <lm:user>kubi</lm:user>
            <lm:interfaces>
               <lm:atom>http://yeti.lifemapper.org/services/sdm/layers/atom</lm:atom>
               <lm:html>http://yeti.lifemapper.org/services/sdm/layers/html</lm:html>
               <lm:json>http://yeti.lifemapper.org/services/sdm/layers/json</lm:json>
               <lm:xml>http://yeti.lifemapper.org/services/sdm/layers/xml</lm:xml>
            </lm:interfaces>
            <lm:pages>
               <lm:page href="http://yeti.lifemapper.org/services/sdm/layers/xml/?page=0&amp;amp;perPage=2&amp;amp;fullObjects=0&amp;amp;epsgCode=4326&amp;amp;afterTime=&amp;amp;beforeTime=" rel="first" />
               <lm:page href="http://yeti.lifemapper.org/services/sdm/layers/xml/?page=0&amp;amp;perPage=2&amp;amp;fullObjects=0&amp;amp;epsgCode=4326&amp;amp;afterTime=&amp;amp;beforeTime=" rel="current" />
               <lm:page href="http://yeti.lifemapper.org/services/sdm/layers/xml/?page=1&amp;amp;perPage=2&amp;amp;fullObjects=0&amp;amp;epsgCode=4326&amp;amp;afterTime=&amp;amp;beforeTime=" rel="next" />
               <lm:page href="http://yeti.lifemapper.org/services/sdm/layers/xml/?page=67&amp;amp;perPage=2&amp;amp;fullObjects=0&amp;amp;epsgCode=4326&amp;amp;afterTime=&amp;amp;beforeTime=" rel="last" />
            </lm:pages>
            <lm:items itemCount="134" userId="kubi">
               <lm:queryParameters>
                  <lm:fullObjects>
                     <lm:value>0</lm:value>
                     <lm:param>
                        <lm:displayName>Full Objects</lm:displayName>
                        <lm:name>fullObjects</lm:name>
                        <lm:multiplicity>1</lm:multiplicity>
                        <lm:documentation />
                        <lm:type>integer</lm:type>
                        <lm:options>
                           <lm:option>
                              <lm:name>True</lm:name>
                              <lm:value>1</lm:value>
                           </lm:option>
                           <lm:option>
                              <lm:name>False</lm:name>
                              <lm:value>0</lm:value>
                           </lm:option>
                        </lm:options>
                     </lm:param>
                  </lm:fullObjects>
                  ...
               </lm:queryParameters>
               <lm:item>
                  <lm:description>Precipitation of Driest Month, Predicted 2041-2060 climate calculated from change modeled by Community Climate System Model, 4.0, National Center for Atmospheric Research (NCAR) http://www.cesm.ucar.edu/models/ccsm4.0/ for the IPCC Fifth Assessment Report (2013), Scenario RCP4.5 plus Worldclim 1.4 observed mean climate</lm:description>
                  <lm:epsgcode>4326</lm:epsgcode>
                  <lm:id>7510</lm:id>
                  <lm:modTime>2015-11-19 16:08:10</lm:modTime>
                  <lm:title>cc45bi5014-10min: Precipitation of Driest Month, IPCC AR5 RCP4.5, 2050, 10min</lm:title>
                  <lm:url>http://yeti.lifemapper.org/services/sdm/layers/7510</lm:url>
               </lm:item>
               <lm:item>
                  <lm:description>Precipitation of Warmest Quarter, Predicted 2041-2060 climate calculated from change modeled by Community Climate System Model, 4.0, National Center for Atmospheric Research (NCAR) http://www.cesm.ucar.edu/models/ccsm4.0/ for the IPCC Fifth Assessment Report (2013), Scenario RCP4.5 plus Worldclim 1.4 observed mean climate</lm:description>
                  <lm:epsgcode>4326</lm:epsgcode>
                  <lm:id>7509</lm:id>
                  <lm:modTime>2015-11-19 16:08:10</lm:modTime>
                  <lm:title>cc45bi5018-10min: Precipitation of Warmest Quarter, IPCC AR5 RCP4.5, 2050, 10min</lm:title>
                  <lm:url>http://yeti.lifemapper.org/services/sdm/layers/7509</lm:url>
               </lm:item>
            </lm:items>
         </lm:response>
         
-----

**********
Post Layer
**********
The post layer service allows you to post a new environment layer for use in 
SDM experiments within Lifemapper.

HTTP Method
===========
POST

URL
===
/services/sdm/layers/{format}

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
Layers can be posted with all metadata in an XML document if you provide a layer 
URL where the content can be downloaded.  Otherwise, metadata parameters should 
be included in the URL and the body of the requests should be the layer content.

+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter      | Type     | Required | Description                                                                                                                                                   |
+================+==========+==========+===============================================================================================================================================================+
| name           | String   | Yes      | A short name for this layer, note that this must be unique for each user                                                                                      |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| title          | String   | No       | A title for this layer                                                                                                                                        |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| valUnits       | String   | No       | The units for the values in each cell (ex. degrees Celsius)                                                                                                   |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| startDate      | ISO 8601 | No       | The start date for this layer                                                                                                                                 |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| endDate        | ISO 8601 | No       | The ending date for this layer                                                                                                                                |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| units          | String   | Yes      | The cell size units                                                                                                                                           |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| resolution     | Numeric  | Yes      | The resolution of the cell, in number of (cell) units per cell                                                                                                |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| epsgCode       | Integer  | Yes      | The EPSG code for the layer's map projection                                                                                                                  |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| keyword        | String   | No       | A keyword associated with the layer (add more keyword parameters for multiple keywords ex. keyword=kw1&keyword=kw2                                            |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| envLayerType   | String   | Yes      | The name of the environmental layer type code for this layer                                                                                                  |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| envLayerTypeId | Integer  | No       | The id of the type code for this layer (Client library isn't exposing this, instead just use envLayerType                                                     |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| description    | String   | No       | A description of the layer                                                                                                                                    |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| dataFormat     | String   | Yes      | The format of the layer data - see  http://www.gdal.org/formats_list.html                                                                                     |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| layerUrl       | String   | No       | A URL containing the raster data. If this is provided, you do not need to include the layer data in the body of the request as it will be pulled from the URL |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+
| isCategorical  | Boolean  | No       | Indicates if the layer contains categorical data                                                                                                              |
+----------------+----------+----------+---------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example
=======
Post a new layer with the name 'sampleLayer'.  The data is in EPSG:4326 and the 
cells are 2.5 decimal degrees (dd) with the measurement units degreesC.  The 
data is a GeoTiff and we'll use the 'temperature' type code.  The file is 
located at 'layerData.tif' on the local system.

Request
.. code-block:: bash
      
         $ curl -X POST -H 'Content-type: image/tiff' --data '@layerData.tif' http://svc.lifemapper.org/services/sdm/layers/?name=sampleLayer&units=dd&resolution=2.5&epsgCode=4326&envLayerType=temperature&dataFormat=GTiff&valUnits=degreesC


Response:
     The response of this request is the same as if you ran a GET request on the 
     layer you just posted.  

-----

************
Layer Object
************

Sample JSON

.. code-block:: json

         {
            "title": "Precipitation Seasonality, IPCC AR5 RCP4.5, 2050, 10min",
            "SRS": "epsg:4326",
            "bbox": "(-180.0, -60.0, 180.0, 90.0)",
            "dataFormat": "GTiff",
            "description": "Precipitation Seasonality (Coefficient of Variation), Predicted 2041-2060 climate calculated from change modeled by Community Climate System Model, 4.0, National Center for Atmospheric Research (NCAR) http://www.cesm.ucar.edu/models/ccsm4.0/ for the IPCC Fifth Assessment Report (2013), Scenario RCP4.5 plus Worldclim 1.4 observed mean climate",
            "endDate": "1864-07-08 00:00:00",
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
            "id": "7513",
            "isCategorical": "False",
            "keywords": 
            {
               "keyword": "precipitation",
               "keyword": "seasonality"
            },
            "mapLayername": "cc45bi5015-10min",
            "mapPrefix": "http://yeti.lifemapper.org/ogc?map=usr_kubi_4326&layers=cc45bi5015-10min",
            "mapUnits": "dd",
            "maxVal": "222.0",
            "maxX": "180.0",
            "maxY": "90.0",
            "metadataUrl": "http://yeti.lifemapper.org/services/sdm/layers/7513",
            "minVal": "0.0",
            "minX": "-180.0",
            "minY": "-60.0",
            "modTime": "2015-11-19 16:08:10",
            "moduleType": "sdm",
            "name": "cc45bi5015-10min",
            "nodataVal": "-32768.0",
            "parametersModTime": "2015-11-19 16:08:10",
            "resolution": "0.16667",
            "serviceType": "layers",
            "size": 
            {
               "size": "2160",
               "size": "900"
            },
            "srs": "GEOGCS['WGS 84',DATUM['unknown',SPHEROID['WGS84',6378137,298.257223563],TOWGS84[0,0,0,0,0,0,0]],PRIMEM['Greenwich',0],UNIT['degree',0.0174532925199433]]",
            "startDate": "1864-06-19 00:00:00",
            "title": "Precipitation Seasonality, IPCC AR5 RCP4.5, 2050, 10min",
            "typeCode": "BIO15",
            "typeDescription": "Precipitation Seasonality (Coefficient of Variation)",
            "typeKeywords": 
            {
               "typeKeyword": "precipitation",
               "typeKeyword": "seasonality"
            },
            "typeTitle": "Precipitation Seasonality",
            "user": "kubi",
            "valUnits": "coefficientOfVariation",
            "verify": "6be49375f7f57e1da5c6683624f5e2b3ee39807e986d1582e901cac38caec5c3"
         }
