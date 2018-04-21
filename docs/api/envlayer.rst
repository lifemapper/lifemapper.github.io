================================
Environmental Layer REST Service
================================

.. contents::  

The Lifemapper SDM Type Codes REST service allows a user to count, list, post, 
get, and delete environmental layers that are used in scenarios.

****************
Count Type Codes
****************
Requests sent to the type codes count service will return the number of 
environmental layers that match the specified criteria for the specified user.

HTTP Method
===========
GET

URL
===
/api/v2/envlayer/count/{format}

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

+------------+--------------------+------------+-----------------------------------------------------------------+
| Name       | Type               | Example    | Description                                                     |
+============+====================+============+=================================================================+
| afterTime  | ISO 8601 Date time | 2015-05-13 | Count type codes modified after this time                       |
+------------+--------------------+------------+-----------------------------------------------------------------+
| beforeTime | ISO 8601 Date time | 2014-12-03 | Count type codes modified before this time                      |
+------------+--------------------+------------+-----------------------------------------------------------------+
| public     | Integer            | 1          | (Only if logged in) Count public type codes if this is set to 1 |
+------------+--------------------+------------+-----------------------------------------------------------------+

Example
=======
For this example, we will count all of the type codes in the system.

Request::

      $ curl "http://svc.lifemapper.org/services/sdm/typecodes/count/json"

Response
   
.. code-block:: json

   {
      "title": "Lifemapper List Service",
      "denominator": "1",
      "imag": "0",
      "numerator": "20",
      "real": "20"
   }

-----

****************
Delete Type Code
****************
The delete type code service removes a type code you own from the Lifemapper system.  

HTTP Method
===========
DELETE

URL
===
/api/v2/envlayer/{type code id}

Example
=======
For this example, we will delete type code 100

Request::

   $ curl -X DELETE "http://svc.lifemapper.org/api/v2/envlayer/100"

-----

*************
Get Type Code
*************
The get type code method retrieves a type code that you own or that is public.

HTTP Method
===========
GET

URL
===
/services/sdm/typecodes/{type code id}/{format}

Format Options
==============
+---------+----------------------+----------------------------------------------------+
| Format  | Content-Type         | Description                                        |
+=========+======================+====================================================+
| (blank) | text/html            | Returns an HTML page containing type code metadata |
+---------+----------------------+----------------------------------------------------+
| atom    | application/atom+xml | Returns an atom feed for the type code             |
+---------+----------------------+----------------------------------------------------+
| html    | text/html            | Returns an HTML page containing type code metadata |
+---------+----------------------+----------------------------------------------------+
| json    | application/json     | Returns a JSON document with type code metadata    |
+---------+----------------------+----------------------------------------------------+
| xml     | application/xml      | Returns an XML document with type code metadata    |
+---------+----------------------+----------------------------------------------------+


Example
=======
For this example, we will get the metadata for type code 131 XML format
   
Request::

   $ curl -X GET "http://svc.lifemapper.org/services/sdm/typecodes/131/xml"

Response::

   <?xml version="1.0" encoding="utf-8"?>
   <?xml-stylesheet type="text/xsl" href="/css/services.xsl?r=20140721"?>
   <lm:response xmlns:lm="http://lifemapper.org" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://lifemapper.org /schemas/serviceResponse.xsd">
      <lm:title>Lifemapper typecode 131</lm:title>
      <lm:user>kubi</lm:user>
      <lm:typecode>
         <lm:createTime>2015-11-18 20:41:01</lm:createTime>
         <lm:id>131</lm:id>
         <lm:metadataUrl>http://yeti.lifemapper.org/services/sdm/typecodes/131</lm:metadataUrl>
         <lm:modTime>2015-11-18 20:41:01</lm:modTime>
         <lm:moduleType>sdm</lm:moduleType>
         <lm:parametersModTime>2015-11-18 20:41:01</lm:parametersModTime>
         <lm:serviceType>typecodes</lm:serviceType>
         <lm:typeCode>BIO19</lm:typeCode>
         <lm:typeDescription>Precipitation of Coldest Quarter</lm:typeDescription>
         <lm:typeKeywords>
            <lm:typeKeyword>precipitation</lm:typeKeyword>
            <lm:typeKeyword>coldest quarter</lm:typeKeyword>
         </lm:typeKeywords>
         <lm:typeTitle>Precipitation of Coldest Quarter</lm:typeTitle>
         <lm:user>kubi</lm:user>
      </lm:typecode>
   </lm:response>

-----


***************
List Type Codes
***************
The type codes listing services allows you to retrieve a list of Lifemapper type codes that meet your specified criteria.  The "page" and "perPage" parameters provide a method to page through results since they are often too numerous to retrieve with one request

HTTP Method
===========
GET

URL
===
/services/sdm/typecodes/{format}

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
+-------------+--------------------+------------+------------------------------------------------------------------------------------+
| Name        | Type               | Example    | Description                                                                        |
+=============+====================+============+====================================================================================+
| afterTime   | ISO 8601 Date time | 2015-05-13 | Return type codes modified after this time                                         |
+-------------+--------------------+------------+------------------------------------------------------------------------------------+
| beforeTime  | ISO 8601 Date time | 2014-12-03 | Return type codes modified before this time                                        |
+-------------+--------------------+------------+------------------------------------------------------------------------------------+
| fullObjects | Integer            | 0          | If this is 1, return all object metadata, if it is 0, return small versions (less) |
+-------------+--------------------+------------+------------------------------------------------------------------------------------+
| page        | Integer            | 3          | Return this page of results (zero-based count)                                     |
+-------------+--------------------+------------+------------------------------------------------------------------------------------+
| perPage     | Integer            | 100        | Return this many results per page                                                  |
+-------------+--------------------+------------+------------------------------------------------------------------------------------+
| public      | Integer            | 1          | (Only if logged in) Return public type codes if this is set to 1                   |
+-------------+--------------------+------------+------------------------------------------------------------------------------------+



Example
=======
In this example, we will request the 0th page of results with 3 results per page as an ATOM feed

Request::

   $ curl -X GET "http://svc.lifemapper.org/services/sdm/typecodes/atom?page=0&perPage=3"

Response

.. code-block:: xml

   <feed xmlns="http://www.w3.org/2005/Atom">
      <id>http://yeti.lifemapper.org/services/sdm/typecodes/atom</id>
      <title>Lifemapper List Service</title>
      <link href="http://yeti.lifemapper.org/services/sdm/typecodes/atom" rel="self" />
      <updated>2016-08-22T19:20:38Z</updated>
      <author>
         <name>Lifemapper</name>
         <email>no-reply-lifemapper@yeti.lifemapper.org</email>
      </author>
      <link href="http://yeti.lifemapper.org/services/sdm/typecodes/atom/?page=0&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="first" />
      <link href="http://yeti.lifemapper.org/services/sdm/typecodes/atom/?page=0&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="current" />
      <link href="http://yeti.lifemapper.org/services/sdm/typecodes/atom/?page=1&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="next" />
      <link href="http://yeti.lifemapper.org/services/sdm/typecodes/atom/?page=6&amp;amp;amp;perPage=3&amp;amp;amp;fullObjects=0&amp;amp;amp;afterTime=&amp;amp;amp;beforeTime=" rel="last" />
      <entry>
         <id>http://yeti.lifemapper.org/services/sdm/typecodes/1886</id>
         <link href="http://yeti.lifemapper.org/services/sdm/typecodes/1886/atom" rel="self" />
         <link href="http://yeti.lifemapper.org/services/sdm/typecodes/1886/atom" rel="alternate" />
         <title>ALT: Elevation</title>
         <updated>2015-11-19T16:08:10Z</updated>
         <summary>ALT: Elevation</summary>
      </entry>
      <entry>
         <id>http://yeti.lifemapper.org/services/sdm/typecodes/1879</id>
         <link href="http://yeti.lifemapper.org/services/sdm/typecodes/1879/atom" rel="self" />
         <link href="http://yeti.lifemapper.org/services/sdm/typecodes/1879/atom" rel="alternate" />
         <title>BIO1: Annual Mean Temperature</title>
         <updated>2015-11-19T16:08:10Z</updated>
         <summary>BIO1: Annual Mean Temperature</summary>
      </entry>
      <entry>
         <id>http://yeti.lifemapper.org/services/sdm/typecodes/130</id>
         <link href="http://yeti.lifemapper.org/services/sdm/typecodes/130/atom" rel="self" />
         <link href="http://yeti.lifemapper.org/services/sdm/typecodes/130/atom" rel="alternate" />
         <title>BIO10: Mean Temperature of Warmest Quarter</title>
         <updated>2015-11-18T20:41:01Z</updated>
         <summary>BIO10: Mean Temperature of Warmest Quarter</summary>
      </entry>
   </feed> 
        
-----

**************
Post Type Code
**************
The post type code service allows you to post a new layer type code within Lifemapper

HTTP Method
===========
POST

URL
===
/services/sdm/typecodes/{format}

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

+-------------+--------+----------+-------------------------------------------------------------------------------------------------------------------------+
| Parameter   | Type   | Required | Description                                                                                                             |
+=============+========+==========+=========================================================================================================================+
| code        | String | Yes      | A short name for the type code                                                                                          |
+-------------+--------+----------+-------------------------------------------------------------------------------------------------------------------------+
| description | String | No       | A longer description of the type code                                                                                   |
+-------------+--------+----------+-------------------------------------------------------------------------------------------------------------------------+
| keyword     | String | No       | A keyword associated with the type code (add more keyword parameters for multiple keywords ex. keyword=kw1&keyword=kw2) |
+-------------+--------+----------+-------------------------------------------------------------------------------------------------------------------------+
| title       | String | No       | A title for the type code                                                                                               |
+-------------+--------+----------+-------------------------------------------------------------------------------------------------------------------------+


Example
=======
Post a new type code with code: sample, description: A sample type code

Request::
     
   $ curl -X POST http://svc.lifemapper.org/services/sdm/typecodes/?code=sample&description=A%20sample%20type%20code

Response::

   The response of this request is the same as if you ran a GET request on the type code you just posted.  

-----

****************
Type Code Object
****************

Sample JSON

.. code-block:: json

   
   {
      "title": "Lifemapper typecode 1886",
      "createTime": "2015-11-19 16:08:10",
      "id": "1886",
      "metadataUrl": "http://yeti.lifemapper.org/services/sdm/typecodes/1886",
      "modTime": "2015-11-19 16:08:10",
      "moduleType": "sdm",
      "parametersModTime": "2015-11-19 16:08:10",
      "serviceType": "typecodes",
      "typeCode": "ALT",
      "typeDescription": "Worldclim Elevation (altitude above sea level, from SRTM, http://www2.jpl.nasa.gov/srtm/)",
      "typeKeywords": 
      {
         "typeKeyword": "elevation"
      },
      "typeTitle": "Elevation",
      "user": "kubi"
   }
   