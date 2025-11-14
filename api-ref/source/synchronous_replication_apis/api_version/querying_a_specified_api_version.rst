:original_name: sdrs_05_0202.html

.. _sdrs_05_0202:

Querying a Specified API Version
================================

Function
--------

This API is used to query a specified API version.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /{api_version}

-  Parameter description

   =========== ========= ===============================================
   Parameter   Mandatory Description
   =========== ========= ===============================================
   api_version Yes       Specifies the API version, for example, **v1**.
   =========== ========= ===============================================

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{endpoint}/v1

Response
--------

-  Parameter description

   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                          |
   +=======================+=======================+======================================================================+
   | version               | Object                | Specifies the version of an API.                                     |
   |                       |                       |                                                                      |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0202__table14672161881114>`. |
   +-----------------------+-----------------------+----------------------------------------------------------------------+

   .. _sdrs_05_0202__table14672161881114:

   .. table:: **Table 1** **version** field description

      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                                                                                                                               |
      +=======================+=======================+===========================================================================================================================================================================================================+
      | id                    | String                | Specifies the version ID, for example, **v1**.                                                                                                                                                            |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | links                 | Array of objects      | Specifies the API URL.                                                                                                                                                                                    |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | For details, see :ref:`Table 2 <sdrs_05_0202__table122284216266>`.                                                                                                                                        |
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
      | updated               | String                | Specifies the version release time, which must be the UTC time. For example, the release time of v1 is 2018-05-30T15:00:00Z.                                                                              |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | min_version           | String                | Specifies the microversion. If APIs of a version support microversions, the system returns the supported minimum microversion. If microversions are not supported, the system returns an empty value.     |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0202__table122284216266:

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
          "version": {
              "id": "v1",
              "links": [
                  {
                      "href": "https://sdrs.localdomain.com/v1",
                      "rel": "self"
                  }
              ],
              "status": "CURRENT",
              "updated": "2018-05-30T00:00:00Z",
              "version": "",
              "min_version": ""
          }
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
