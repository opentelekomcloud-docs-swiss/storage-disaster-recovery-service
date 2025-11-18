:original_name: sdrs_05_0201.html

.. _sdrs_05_0201:

Querying API Versions
=====================

Function
--------

This API is used to query all available API versions of SDRS.

Constraints
-----------

None

URI
---

-  URI format

   GET /

Request
-------

-  Parameter description

   None

-  Example request

   GET https://{endpoint}/

Response
--------

-  Parameter description

   +-----------------------+-----------------------+-------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                       |
   +=======================+=======================+===================================================================+
   | versions              | Array of objects      | Specifies the API version list.                                   |
   |                       |                       |                                                                   |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0201__table11250550892>`. |
   +-----------------------+-----------------------+-------------------------------------------------------------------+

   .. _sdrs_05_0201__table11250550892:

   .. table:: **Table 1** **versions** field description

      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                                                                                                                               |
      +=======================+=======================+===========================================================================================================================================================================================================+
      | id                    | String                | Specifies the version ID, for example, **v1**.                                                                                                                                                            |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | links                 | Array of objects      | Specifies the API URL.                                                                                                                                                                                    |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | For details, see :ref:`Table 2 <sdrs_05_0201__en-us_topic_0060111075_table35183803523>`.                                                                                                                  |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | version               | String                | Specifies the version. If the APIs of this version support microversions, the system returns the supported maximum microversion. If the microversion is not supported, the system returns an empty value. |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | status                | String                | Specifies the version status. Values are as follows:                                                                                                                                                      |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | **CURRENT**: widely used version                                                                                                                                                                          |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | **SUPPORT**: earlier version which is still supported                                                                                                                                                     |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | **DEPRECATED**: deprecated version which may be deleted later                                                                                                                                             |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | updated               | String                | Specifies the version release time in UTC format. For example, the release time of v1 is 2018-05-30T15:00:00Z.                                                                                            |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | min_version           | String                | Specifies the microversion. If APIs of a version support microversions, the system returns the supported minimum microversion. If microversions are not supported, the system returns an empty value.     |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0201__en-us_topic_0060111075_table35183803523:

   .. table:: **Table 2** **links** parameters

      ========= ====== =================================
      Parameter Type   Description
      ========= ====== =================================
      rel       String Describes a link.
      href      String Specifies the version query link.
      ========= ====== =================================

-  Example response

   .. code-block::

      {
          "versions": [
              {
                  "id": "v1",
                  "links": [
                      {
                          "href": "https://sdrs.localdomain.com/v1",
                          "rel": "self"
                      }
                  ],
                  "status": "CURRENT",
                  "updated": "2018-05-30T15:00:00Z",
                  "version": "",
                  "min_version": ""
              }
          ]
      }

   Or

   .. code-block::

      {
            "error": {
                "message": "XXXX",
                "code": "XXX"
            }
        }

   In the preceding example, **error** indicates a general error, for example, **badrequest** or **itemNotFound**. An example is provided as follows:

   .. code-block::

      {
            "badrequest": {
                "message": "XXXX",
                "code": "XXX"
            }
        }

**Returned Value**
------------------

-  Normal

   ============== ====================================
   Returned Value Description
   ============== ====================================
   200            The server has accepted the request.
   ============== ====================================

-  Abnormal

   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | Returned Value                    | Description                                                                                             |
   +===================================+=========================================================================================================+
   | 400 Bad Request                   | The server failed to process the request.                                                               |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 401 Unauthorized                  | You must enter a username and the password to access the requested page.                                |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 403 Forbidden                     | You are forbidden to access the requested page.                                                         |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 404 Not Found                     | The server could not find the requested page.                                                           |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 405 Method Not Allowed            | You are not allowed to use the method specified in the request.                                         |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 406 Not Acceptable                | The response generated by the server could not be accepted by the client.                               |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 407 Proxy Authentication Required | You must use the proxy server for authentication so that the request can be processed.                  |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 408 Request Timeout               | The request timed out.                                                                                  |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 409 Conflict                      | The request could not be processed due to a conflict.                                                   |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 500 Internal Server Error         | Failed to complete the request because of a service error.                                              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 501 Not Implemented               | Failed to complete the request because the server does not support the requested function.              |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 502 Bad Gateway                   | Failed to complete the request because the server receives an invalid response from an upstream server. |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 503 Service Unavailable           | Failed to complete the request because the system is unavailable.                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
   | 504 Gateway Timeout               | A gateway timeout error occurred.                                                                       |
   +-----------------------------------+---------------------------------------------------------------------------------------------------------+
