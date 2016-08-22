
.. highlight:: rest

============================
SDM Experiments REST Service
============================

.. contents::  


The Lifemapper SDM Experiments REST service allows a user to count, list, post, get, and delete Species Distribution Modeling experiments.

*****************
Count Experiments
*****************
Requests sent to the experiment count service will return the number of SDM experiments that match the specified criteria for the specified user.

HTTP Method
===========
GET

URL
===
/services/sdm/experiments/count/{format}

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

   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | Name            | Type               | Example     | Description                                                                         |
   +=================+====================+=============+=====================================================================================+
   | afterTime       | ISO 8601 Date time | 2015-05-13  | Count experiments modified after this time                                          |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | algorithmCode   | String             | ATT_MAXENT  | Count experiments where the model used this algorithm                               |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | beforeTime      | ISO 8601 Date time | 2014-12-03  | Count experiments modified before this time                                         |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | displayName     | String             | Boops boops | Count experiments where the occurrence set used this display name (wildcard search) |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | epsgCode        | Integer            | 4326        | Count experiments built using this EPSG code                                        |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | occurrenceSetId | Integer            | 123         | Count experiments built using this occurrence set id                                |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | status          | Integer            | 300         | Count experiments that have this model status                                       |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+
   | public          | Integer            | 1           | (Only if logged in) Count public experiments if this is set to 1                    |
   +-----------------+--------------------+-------------+-------------------------------------------------------------------------------------+

Example
=======
   For this example, we will count all of the public experiments built with the ATT Maxent algorithm and request a JSON document as the response.

   Request
      $ curl "http://svc.lifemapper.org/services/sdm/experiments/count/json?public=1&algorithmCode=ATT_MAXENT"

   Response
   
      .. code-block:: json

         {
            "title": "Lifemapper List Service",
            "denominator": "1",
            "imag": "0",
            "numerator": "94236",
            "real": "94236"
         }

-----

*****************
Delete Experiment
*****************
   The delete experiment service removes an experiment you own from the Lifemapper system.  You may want to do this if you think an experiment is invalid or out of date.

HTTP Method
===========
   DELETE

URL
===
   /services/sdm/experiments/{experiment id}

Example
=======
   For this example, we will delete experiment 12345

   Request
      $ curl -X DELETE "http://svc.lifemapper.org/services/sdm/experiments/12345"

-----

**************
Get Experiment
**************
   The get experiment method retrieves an experiment that you own or that is public.

HTTP Method
===========
   GET

URL
===
   /services/sdm/experiments/{experiment id}/{format}

Format Options
==============
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | Format  | Content-Type                         | Description                                                        |
    +=========+======================================+====================================================================+
    | (blank) | text/html                            | Returns an HTML page containing experiment metadata                |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | atom    | application/atom+xml                 | Returns an atom fed for the experiment                             |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | eml     | application/xml                      | Returns an EML document with experiment metadata                   |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | html    | text/html                            | Returns an HTML page containing experiment metadata                |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | json    | application/json                     | Returns a JSON document with experiment metadata                   |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | kml     | application/vnd.google-earth.kml+xml | Returns a KML document with the spatial layers in the experiment   |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | model   | application/xml or text/plain        | Returns the raw model output from the modeling software            |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | package | application/zip                      | Returns a compressed archive of outputs from the modeling software |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | status  | application/xml                      | Returns an XML document with the status of the experiment          |
    +---------+--------------------------------------+--------------------------------------------------------------------+
    | xml     | application/xml                      | Returns an XML document with experiment metadata                   |
    +---------+--------------------------------------+--------------------------------------------------------------------+




Example
=======
   For this example, we will get the raw model of experiment 12345.  It was built with Maxent and is completed

   Request
      $ curl -X GET "http://svc.lifemapper.org/services/sdm/experiments/12345/model"

   Response

      .. code-block::

         layer0, 0.0, -94.0, 376.0
         layer1, 0.0, 0.0, 3076.0
         layer10, 0.0, -538.0, 257.0
         layer11, 5.519698991509897, 55.0, 724.0
         layer12, 0.0, 112.0, 22527.0
         layer13, 13.044386948399023, -57.0, 488.0
         layer14, 2.3027149788144854, 0.0, 2423.0
         layer15, -51.148340165769405, 0.0, 475.0
         layer16, 0.0, -289.0, 5940.0
         layer17, -6.345070609916794, -446.0, 360.0
         layer18, 0.0, -240.0, 371.0
         layer19, 0.0, 0.0, 254.0
         layer2, 3.3859919784464343, 0.0, 3663.0
         layer3, 0.0, -485.0, 285.0
         layer4, 0.0, 0.0, 1503.0
         layer5, 0.0, 0.0, 1402.0
         layer6, 3.05199595167907, 30.0, 197.0
         layer7, 0.0, 9.0, 94.0
         layer8, 23.035490006361442, 0.0, 8130.0
         layer9, 0.0, -257.0, 308.0
         mask, 0.0, -94.0, 376.0
         layer17^2, -42.26934845965894, 0.0, 198916.0
         layer19^2, -18.344715209346116, 0.0, 64516.0
         layer3^2, -85.49270876421008, 0.0, 235225.0
         linearPredictorNormalizer, 11.504128064671539
         densityNormalizer, 32.962896084594064
         numBackgroundPoints, 10000
         entropy, 5.146361986051062


-----


****************
List Experiments
****************
   The SDM experiments listing services allows you to retrieve a list of Lifemapper experiments that meet your specified criteria.  The "page" and "perPage" parameters provide a method to page through results since they are often too numerous to retrieve with one request

HTTP Method
===========
   GET

URL
===
   /services/sdm/experiments/{format}

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
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | Name            | Type               | Example     | Description                                                                          |
   +=================+====================+=============+======================================================================================+
   | afterTime       | ISO 8601 Date time | 2015-05-13  | Return experiments modified after this time                                          |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | algorithmCode   | String             | ATT_MAXENT  | Return experiments where the model used this algorithm                               |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | beforeTime      | ISO 8601 Date time | 2014-12-03  | Return experiments modified before this time                                         |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | displayName     | String             | Boops boops | Return experiments where the occurrence set used this display name (wildcard search) |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | epsgCode        | Integer            | 4326        | Return experiments built using this EPSG code                                        |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | fullObjects     | Integer            | 0           | If this is 1, return all object metadata, if it is 0, return small versions (less)   |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | occurrenceSetId | Integer            | 123         | Return experiments built using this occurrence set id                                |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | page            | Integer            | 3           | Return this page of results (zero-based count)                                       |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | perPage         | Integer            | 100         | Return this many results per page                                                    |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | status          | Integer            | 300         | Return experiments that have this model status                                       |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+
   | public          | Integer            | 1           | (Only if logged in) Return public experiments if this is set to 1                    |
   +-----------------+--------------------+-------------+--------------------------------------------------------------------------------------+

Example
=======
   In this example, we will request the 5th page of results with 5 results per page.  The experiments should have status 300 for the model (Complete) and be built from data with EPSG: 4326.  The algorithm used to generate the results will be Maxent (ATT_MAXENT)

   Request
      $ curl -X GET "http://svc.lifemapper.org/services/sdm/experiments/json?status=300&perPage=5&algorithmCode=ATT_MAXENT&epsgCode=4326&page=5"

   Response

      .. code-block:: json

         {
            "title": "Lifemapper List Service",
            "items": 
            [
                  {
                     "epsgcode": "4326",
                     "id": "33350",
                     "modTime": "2016-08-12 09:12:00",
                     "title": "Perdita calloleuca",
                     "url": "http://yeti.lifemapper.org/services/sdm/experiments/33350"
                  },
                  {
                     "epsgcode": "4326",
                     "id": "33338",
                     "modTime": "2016-08-12 09:11:59",
                     "title": "Perdita larreae",
                     "url": "http://yeti.lifemapper.org/services/sdm/experiments/33338"
                  },
                  {
                     "epsgcode": "4326",
                     "id": "33340",
                     "modTime": "2016-08-12 09:11:58",
                     "title": "Perdita hirticeps",
                     "url": "http://yeti.lifemapper.org/services/sdm/experiments/33340"
                  },
                  {
                     "epsgcode": "4326",
                     "id": "33342",
                     "modTime": "2016-08-12 09:11:30",
                     "title": "Perdita media",
                     "url": "http://yeti.lifemapper.org/services/sdm/experiments/33342"
                  },
                  {
                     "epsgcode": "4326",
                     "id": "33344",
                     "modTime": "2016-08-12 09:11:30",
                     "title": "Perdita scopata",
                     "url": "http://yeti.lifemapper.org/services/sdm/experiments/33344"
                  }
            ],
            "itemCount": "92308",
            "userId": "kubi",
            "queryParameters": 
            {
               ...(removed for brevity)...
            }
         }

-----

***************
Post Experiment
***************
   The post experiment service allows you to submit a new SDM experiment to Lifemapper for computation

HTTP Method
===========
   POST

URL
===
   /services/sdm/experiments/{format}

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


Example
=======
   Post a new experiment using Bioclim with a standard deviation cutoff value of 1.0.  Build with occurrence set 1234, model scenario 99, and project with scenarios 8, 17, 99, and 342.  Return XML.

   Request
      .. code-block:: bash

         $ curl -X POST -H 'Content-type: application/xml' -d '<lm:request xmlns:lm="http://lifemapper.org" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://lifemapper.org /schemas/serviceRequest.xsd"><lm:experiment><lm:algorithm><lm:algorithmCode>BIOCLIM</lm:algorithmCode><lm:parameters><lm:standarddeviationcutoff>1.0</lm:standarddeviationcutoff></lm:parameters></lm:algorithm><lm:occurrenceSetId>1234</lm:occurrenceSetId><lm:modelScenario>99</lm:modelScenario><lm:name>Sample Experiment</lm:name><lm:description>This is a sample request for posting an experiment</lm:description><lm:projectionScenario>8</lm:projectionScenario><lm:projectionScenario>17</lm:projectionScenario><lm:projectionScenario>99</lm:projectionScenario><lm:projectionScenario>342</lm:projectionScenario></lm:experiment></lm:request>' http://svc.lifemapper.org/services/sdm/experiments/xml

   Response
     The response of this request is the same as if you ran a GET request on the experiment you just posted.  

-----

*****************
Experiment Object
*****************

   Sample XML (extra layers and projections removed)

      .. code-block:: xml

         <?xml version="1.0" encoding="utf-8"?>
         <lm:response xmlns:lm="http://lifemapper.org" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://lifemapper.org /schemas/serviceResponse.xsd">
            <lm:title>Lifemapper experiment 33338</lm:title>
            <lm:user>kubi</lm:user>
            <lm:interfaces>
               <lm:atom>http://yeti.lifemapper.org/services/sdm/experiments/33338/atom</lm:atom>
               <lm:html>http://yeti.lifemapper.org/services/sdm/experiments/33338/html</lm:html>
               <lm:json>http://yeti.lifemapper.org/services/sdm/experiments/33338/json</lm:json>
               <lm:kml>http://yeti.lifemapper.org/services/sdm/experiments/33338/kml</lm:kml>
               <lm:model>http://yeti.lifemapper.org/services/sdm/experiments/33338/model</lm:model>
               <lm:package>http://yeti.lifemapper.org/services/sdm/experiments/33338/package</lm:package>
               <lm:prov>http://yeti.lifemapper.org/services/sdm/experiments/33338/prov</lm:prov>
               <lm:status>http://yeti.lifemapper.org/services/sdm/experiments/33338/status</lm:status>
               <lm:xml>http://yeti.lifemapper.org/services/sdm/experiments/33338/xml</lm:xml>
            </lm:interfaces>
            <lm:experiment>
               <lm:algorithm>
                  <lm:code>ATT_MAXENT</lm:code>
                  <lm:parameters>
                     <lm:responsecurves>0</lm:responsecurves>
                     <lm:verbose>0</lm:verbose>
                     <lm:appendtoresultsfile>0</lm:appendtoresultsfile>
                     <lm:jackknife>0</lm:jackknife>
                     <lm:outputformat>1</lm:outputformat>
                     <lm:replicates>1</lm:replicates>
                     <lm:writebackgroundpredictions>0</lm:writebackgroundpredictions>
                     <lm:threshold>1</lm:threshold>
                     <lm:beta_hinge>-1.0</lm:beta_hinge>
                     <lm:writeplotdata>0</lm:writeplotdata>
                     <lm:fadebyclamping>0</lm:fadebyclamping>
                     <lm:applythresholdrule>0</lm:applythresholdrule>
                     <lm:lq2lqptthreshold>80</lm:lq2lqptthreshold>
                     <lm:beta_threshold>-1.0</lm:beta_threshold>
                     <lm:pictures>1</lm:pictures>
                     <lm:responsecurvesexponent>0</lm:responsecurvesexponent>
                     <lm:l2lqthreshold>10</lm:l2lqthreshold>
                     <lm:extrapolate>1</lm:extrapolate>
                     <lm:quadratic>1</lm:quadratic>
                     <lm:maximumiterations>500</lm:maximumiterations>
                     <lm:hingethreshold>15</lm:hingethreshold>
                     <lm:logscale>1</lm:logscale>
                     <lm:product>1</lm:product>
                     <lm:writemess>1</lm:writemess>
                     <lm:linear>1</lm:linear>
                     <lm:replicatetype>0</lm:replicatetype>
                     <lm:doclamp>1</lm:doclamp>
                     <lm:convergencethreshold>0.00001</lm:convergencethreshold>
                     <lm:maximumbackground>10000</lm:maximumbackground>
                     <lm:plots>1</lm:plots>
                     <lm:adjustsampleradius>0</lm:adjustsampleradius>
                     <lm:hinge>1</lm:hinge>
                     <lm:outputgrids>1</lm:outputgrids>
                     <lm:autofeature>1</lm:autofeature>
                     <lm:randomseed>0</lm:randomseed>
                     <lm:beta_categorical>-1.0</lm:beta_categorical>
                     <lm:randomtestpoints>0</lm:randomtestpoints>
                     <lm:betamultiplier>1.0</lm:betamultiplier>
                     <lm:perspeciesresults>0</lm:perspeciesresults>
                     <lm:allowpartialdata>0</lm:allowpartialdata>
                     <lm:addsamplestobackground>0</lm:addsamplestobackground>
                     <lm:writeclampgrid>1</lm:writeclampgrid>
                     <lm:addallsamplestobackground>0</lm:addallsamplestobackground>
                     <lm:beta_lqp>-1.0</lm:beta_lqp>
                     <lm:removeduplicates>1</lm:removeduplicates>
                     <lm:defaultprevalence>0.5</lm:defaultprevalence>
                  </lm:parameters>
               </lm:algorithm>
               <lm:bbox>(-180.0, -60.0, 180.0, 90.0)</lm:bbox>
               <lm:createTime>2015-11-21 01:37:54</lm:createTime>
               <lm:epsgcode>4326</lm:epsgcode>
               <lm:id>33338</lm:id>
               <lm:metadataUrl>http://yeti.lifemapper.org/services/sdm/experiments/33338</lm:metadataUrl>
               <lm:modTime>2016-08-12 09:11:59</lm:modTime>
               <lm:model>
                  <lm:algorithmCode>ATT_MAXENT</lm:algorithmCode>
                  <lm:bbox>(-180.0, -60.0, 180.0, 90.0)</lm:bbox>
                  <lm:createTime>2015-11-21 01:37:54</lm:createTime>
                  <lm:epsgcode>4326</lm:epsgcode>
                  <lm:id>33338</lm:id>
                  <lm:layers>
                     <lm:layer>
                        <lm:SRS>epsg:4326</lm:SRS>
                        <lm:bbox>(-180.0, -60.0, 180.0, 90.0)</lm:bbox>
                        <lm:dataFormat>GTiff</lm:dataFormat>
                        <lm:description>Mean Temperature of Warmest Quarter, WorldClim 1.4 elevation and bioclimatic variables computed from interpolated observation data collected between 1950 and 2000 (http://www.worldclim.org/), 5 min resolution</lm:description>
                        <lm:endDate>1864-05-09 00:00:00</lm:endDate>
                        <lm:epsgcode>4326</lm:epsgcode>
                        <lm:gdalType>3</lm:gdalType>
                        <lm:geoTransform>
                           <lm:geoTransform>-180.0</lm:geoTransform>
                           <lm:geoTransform>0.166666666667</lm:geoTransform>
                           <lm:geoTransform>0.0</lm:geoTransform>
                           <lm:geoTransform>90.0</lm:geoTransform>
                           <lm:geoTransform>0.0</lm:geoTransform>
                           <lm:geoTransform>-0.166666666667</lm:geoTransform>
                        </lm:geoTransform>
                        <lm:id>7380</lm:id>
                        <lm:isCategorical>False</lm:isCategorical>
                        <lm:keywords>
                           <lm:keyword>warmest quarter</lm:keyword>
                           <lm:keyword>temperature</lm:keyword>
                           <lm:keyword>mean</lm:keyword>
                        </lm:keywords>
                        <lm:mapLayername>bio10-10min</lm:mapLayername>
                        <lm:mapPrefix>http://yeti.lifemapper.org/ogc?map=usr_kubi_4326&amp;amp;layers=bio10-10min</lm:mapPrefix>
                        <lm:mapUnits>dd</lm:mapUnits>
                        <lm:maxVal>380.0</lm:maxVal>
                        <lm:maxX>180.0</lm:maxX>
                        <lm:maxY>90.0</lm:maxY>
                        <lm:metadataUrl>http://yeti.lifemapper.org/services/sdm/layers/7380</lm:metadataUrl>
                        <lm:minVal>-97.0</lm:minVal>
                        <lm:minX>-180.0</lm:minX>
                        <lm:minY>-60.0</lm:minY>
                        <lm:modTime>2015-11-19 16:08:10</lm:modTime>
                        <lm:moduleType>sdm</lm:moduleType>
                        <lm:name>bio10-10min</lm:name>
                        <lm:nodataVal>-9999.0</lm:nodataVal>
                        <lm:parametersModTime>2015-11-18 20:41:01</lm:parametersModTime>
                        <lm:resolution>0.16667</lm:resolution>
                        <lm:serviceType>layers</lm:serviceType>
                        <lm:size>
                           <lm:size>2160</lm:size>
                           <lm:size>900</lm:size>
                        </lm:size>
                        <lm:srs>GEOGCS[&amp;quot;WGS 84&amp;quot;,DATUM[&amp;quot;WGS_1984&amp;quot;,SPHEROID[&amp;quot;WGS 84&amp;quot;,6378137,298.257223563,AUTHORITY[&amp;quot;EPSG&amp;quot;,&amp;quot;7030&amp;quot;]],AUTHORITY[&amp;quot;EPSG&amp;quot;,&amp;quot;6326&amp;quot;]],PRIMEM[&amp;quot;Greenwich&amp;quot;,0],UNIT[&amp;quot;degree&amp;quot;,0.0174532925199433],AUTHORITY[&amp;quot;EPSG&amp;quot;,&amp;quot;4326&amp;quot;]]</lm:srs>
                        <lm:startDate>1864-03-20 00:00:00</lm:startDate>
                        <lm:title>Mean Temperature of Warmest Quarter, Worldclim 1.4, 10min</lm:title>
                        <lm:typeCode>BIO10</lm:typeCode>
                        <lm:typeDescription>Mean Temperature of Warmest Quarter</lm:typeDescription>
                        <lm:typeKeywords>
                           <lm:typeKeyword>warmest quarter</lm:typeKeyword>
                           <lm:typeKeyword>temperature</lm:typeKeyword>
                           <lm:typeKeyword>mean</lm:typeKeyword>
                        </lm:typeKeywords>
                        <lm:typeTitle>Mean Temperature of Warmest Quarter</lm:typeTitle>
                        <lm:user>kubi</lm:user>
                        <lm:valUnits>degreesCelsiusTimes10</lm:valUnits>
                        <lm:verify>d09871275c55f7d34f90e957a9c3438834f0c5e507b1cdc5b2328d2b2b58024b</lm:verify>
                     </lm:layer>
                     ...
                  </lm:layers>
                  <lm:makeflowFilename>/share/lmserver/data/archive/kubi/000/005/831/805/occ_5831805.mf</lm:makeflowFilename>
                  <lm:mapFilename>/share/lmserver/data/archive/kubi/000/005/831/805/data_5831805.map</lm:mapFilename>
                  <lm:mapName>data_5831805</lm:mapName>
                  <lm:metadataUrl>http://yeti.lifemapper.org/services/sdm/models/33338</lm:metadataUrl>
                  <lm:modTime>2016-08-12 09:11:59</lm:modTime>
                  <lm:moduleType>sdm</lm:moduleType>
                  <lm:name>Perdita larreae</lm:name>
                  <lm:occurrenceSet>
                     <lm:SRS>epsg:4326</lm:SRS>
                     <lm:bbox>(-117.63, 31.35, -106.61, 37.29)</lm:bbox>
                     <lm:count>499</lm:count>
                     <lm:dataFormat>ESRI Shapefile</lm:dataFormat>
                     <lm:displayName>Perdita larreae</lm:displayName>
                     <lm:epsgcode>4326</lm:epsgcode>
                     <lm:featureCount>499</lm:featureCount>
                     <lm:feature />
                     <lm:fromGbif>True</lm:fromGbif>
                     <lm:id>5831805</lm:id>
                     <lm:isCategorical>False</lm:isCategorical>
                     <lm:keywords />
                     <lm:layerName>occ_5831805</lm:layerName>
                     <lm:makeflowFilename>/share/lmserver/data/archive/kubi/000/005/831/805/occ_5831805.mf</lm:makeflowFilename>
                     <lm:mapFilename>/share/lmserver/data/archive/kubi/000/005/831/805/data_5831805.map</lm:mapFilename>
                     <lm:mapLayername>occ_5831805</lm:mapLayername>
                     <lm:mapName>data_5831805</lm:mapName>
                     <lm:mapPrefix>http://yeti.lifemapper.org/ogc?map=data_5831805&amp;amp;layers=occ_5831805</lm:mapPrefix>
                     <lm:mapUnits />
                     <lm:maxX>-106.61</lm:maxX>
                     <lm:maxY>37.29</lm:maxY>
                     <lm:metadataUrl>http://yeti.lifemapper.org/services/sdm/occurrences/5831805</lm:metadataUrl>
                     <lm:minX>-117.63</lm:minX>
                     <lm:minY>31.35</lm:minY>
                     <lm:modTime>2016-08-12 08:11:12</lm:modTime>
                     <lm:moduleType>sdm</lm:moduleType>
                     <lm:name>occ_5831805</lm:name>
                     <lm:objId>5831805</lm:objId>
                     <lm:ogrType>1</lm:ogrType>
                     <lm:parametersModTime>2016-08-12 08:11:12</lm:parametersModTime>
                     <lm:queryCount>499</lm:queryCount>
                     <lm:serviceType>occurrences</lm:serviceType>
                     <lm:status>300</lm:status>
                     <lm:statusModTime>2016-08-12 08:11:12</lm:statusModTime>
                     <lm:title>Perdita larreae</lm:title>
                     <lm:user>kubi</lm:user>
                     <lm:verify>0e5efc96d865282b29759a4af2ca2d4dd02d30b1382c2cefb1e3ee02a9f6bc10</lm:verify>
                  </lm:occurrenceSet>
                  <lm:pointsName>Perdita larreae</lm:pointsName>
                  <lm:priority>1</lm:priority>
                  <lm:qualityControl />
                  <lm:ruleset>/share/lmserver/data/archive/kubi/000/005/831/805/33338.txt</lm:ruleset>
                  <lm:scenarioCode>WC-10min</lm:scenarioCode>
                  <lm:serviceType>models</lm:serviceType>
                  <lm:status>300</lm:status>
                  <lm:statusModTime>2016-08-12 09:11:59</lm:statusModTime>
                  <lm:user>kubi</lm:user>
               </lm:model>
               <lm:moduleType>sdm</lm:moduleType>
               <lm:projections>
                  <lm:projection>
                     <lm:SRS>epsg:4326</lm:SRS>
                     <lm:algorithmCode>ATT_MAXENT</lm:algorithmCode>
                     <lm:bbox>(-180.0, -60.0, 180.0, 90.0)</lm:bbox>
                     <lm:createTime>2015-11-21 01:37:54</lm:createTime>
                     <lm:dataFormat>GTiff</lm:dataFormat>
                     <lm:description>Predicted habitat for Perdita larreae projected onto WC-10min datalayers</lm:description>
                     <lm:endDate>2000-01-01 00:00:00</lm:endDate>
                     <lm:epsgcode>4326</lm:epsgcode>
                     <lm:gdalType>1</lm:gdalType>
                     <lm:geoTransform>
                        <lm:geoTransform>-180.0</lm:geoTransform>
                        <lm:geoTransform>0.166666666667</lm:geoTransform>
                        <lm:geoTransform>0.0</lm:geoTransform>
                        <lm:geoTransform>90.0</lm:geoTransform>
                        <lm:geoTransform>0.0</lm:geoTransform>
                        <lm:geoTransform>-0.166666666667</lm:geoTransform>
                     </lm:geoTransform>
                     <lm:id>6707641</lm:id>
                     <lm:isCategorical>False</lm:isCategorical>
                     <lm:keywords>
                        <lm:keyword>bioclimatic variables</lm:keyword>
                        <lm:keyword>climate</lm:keyword>
                        <lm:keyword>elevation</lm:keyword>
                        <lm:keyword>Perdita larreae</lm:keyword>
                        <lm:keyword>habitat model</lm:keyword>
                        <lm:keyword>ATT_MAXENT</lm:keyword>
                        <lm:keyword>observed</lm:keyword>
                        <lm:keyword>present</lm:keyword>
                     </lm:keywords>
                     <lm:layers>
                        <lm:layer>...</lm:layer>
                     </lm:layers>
                     <lm:makeflowFilename>/share/lmserver/data/archive/kubi/000/005/831/805/occ_5831805.mf</lm:makeflowFilename>
                     <lm:mapFilename>/share/lmserver/data/archive/kubi/000/005/831/805/data_5831805.map</lm:mapFilename>
                     <lm:mapLayername>prj_6707641</lm:mapLayername>
                     <lm:mapName>data_5831805</lm:mapName>
                     <lm:mapPrefix>http://yeti.lifemapper.org/ogc?map=data_5831805&amp;amp;layers=prj_6707641</lm:mapPrefix>
                     <lm:mapUnits>dd</lm:mapUnits>
                     <lm:maxVal>100.0</lm:maxVal>
                     <lm:maxX>180.0</lm:maxX>
                     <lm:maxY>90.0</lm:maxY>
                     <lm:metadataUrl>http://yeti.lifemapper.org/services/sdm/projections/6707641</lm:metadataUrl>
                     <lm:minVal>0.0</lm:minVal>
                     <lm:minX>-180.0</lm:minX>
                     <lm:minY>-60.0</lm:minY>
                     <lm:modTime>2016-08-14 14:54:02</lm:modTime>
                     <lm:moduleType>sdm</lm:moduleType>
                     <lm:name>prj_6707641</lm:name>
                     <lm:nodataVal>127.0</lm:nodataVal>
                     <lm:objId>6707641</lm:objId>
                     <lm:parametersModTime>2016-08-14 14:54:02</lm:parametersModTime>
                     <lm:priority>1</lm:priority>
                     <lm:resolution>0.16667</lm:resolution>
                     <lm:scenarioCode>WC-10min</lm:scenarioCode>
                     <lm:serviceType>projections</lm:serviceType>
                     <lm:size>
                        <lm:size>2160</lm:size>
                        <lm:size>900</lm:size>
                     </lm:size>
                     <lm:speciesName>Perdita larreae</lm:speciesName>
                     <lm:srs>GEOGCS[&amp;quot;WGS 84&amp;quot;,DATUM[&amp;quot;WGS_1984&amp;quot;,SPHEROID[&amp;quot;WGS 84&amp;quot;,6378137,298.257223563,AUTHORITY[&amp;quot;EPSG&amp;quot;,&amp;quot;7030&amp;quot;]],AUTHORITY[&amp;quot;EPSG&amp;quot;,&amp;quot;6326&amp;quot;]],PRIMEM[&amp;quot;Greenwich&amp;quot;,0],UNIT[&amp;quot;degree&amp;quot;,0.0174532925199433],AUTHORITY[&amp;quot;EPSG&amp;quot;,&amp;quot;4326&amp;quot;]]</lm:srs>
                     <lm:startDate>1950-01-01 00:00:00</lm:startDate>
                     <lm:status>300</lm:status>
                     <lm:statusModTime>2016-08-14 14:54:02</lm:statusModTime>
                     <lm:title>Perdita larreae Projection 6707641</lm:title>
                     <lm:user>kubi</lm:user>
                     <lm:verify>69254473c30c528fb57ac38ece90b719d7f50aa4d57ed0549629ff00362fa56f</lm:verify>
                  </lm:projection>
                  ...
               </lm:projections>
               <lm:serviceType>experiments</lm:serviceType>
               <lm:statusModTime>2016-08-14 14:54:33</lm:statusModTime>
               <lm:user>kubi</lm:user>
            </lm:experiment>
         </lm:response>


Experiment Subobjects
=====================
   Experiments have subobjects that have their own interfaces and a projections sub service

   * algorithm - Returns algorithm metadata from the model in either atom, html, json, or xml format
   * occurrences - Returns occurrence set metadata from the model in atom, html, json, or xml format
   * scenario - Returns scenario metadata in atom, html, json, or xml format
   * projections - Subservice.  Works like the projections service with the experimentId parameter filled in for this experiment

