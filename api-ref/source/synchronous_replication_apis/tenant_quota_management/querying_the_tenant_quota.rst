:original_name: sdrs_05_1101.html

.. _sdrs_05_1101:

Querying the Tenant Quota
=========================

Function
--------

This API is used to query the tenant quota.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/sdrs/quotas

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{Endpoint}/v1/{project_id}/sdrs/quotas

Response
--------

-  Parameter description

   +-----------------------+-----------------------+----------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                          |
   +=======================+=======================+======================================================================+
   | quotas                | Object                | Specifies the tenant quota information.                              |
   |                       |                       |                                                                      |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_1101__table19635152315164>`. |
   +-----------------------+-----------------------+----------------------------------------------------------------------+

   .. _sdrs_05_1101__table19635152315164:

   .. table:: **Table 1** **quotas** field description

      +-----------------------+-----------------------+-------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                       |
      +=======================+=======================+===================================================================+
      | resources             | Array of objects      | Lists the tenant's resource quota.                                |
      |                       |                       |                                                                   |
      |                       |                       | For details, see :ref:`Table 2 <sdrs_05_1101__table29499002812>`. |
      +-----------------------+-----------------------+-------------------------------------------------------------------+

   .. _sdrs_05_1101__table29499002812:

   .. table:: **Table 2** **resources** field description

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                          |
      +=======================+=======================+======================================================================================+
      | type                  | String                | Specifies the resource type. The value can be **server_groups** or **replications**. |
      |                       |                       |                                                                                      |
      |                       |                       | -  **server_groups**: indicates protection groups.                                   |
      |                       |                       | -  **replications**: indicates replication pairs.                                    |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------+
      | used                  | Integer               | Specifies the number of used resources.                                              |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------+
      | quota                 | Integer               | Specifies the resource quota.                                                        |
      |                       |                       |                                                                                      |
      |                       |                       | If the value is **-1**, the resource is not limited.                                 |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------+
      | min                   | Integer               | Specifies the minimally allowed resource quota.                                      |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------+
      | max                   | Integer               | Specifies the maximally allowed resource quota.                                      |
      |                       |                       |                                                                                      |
      |                       |                       | If the value is **-1**, the resource is not limited.                                 |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
          "quotas": {
              "resources": [
                  {
                      "type": "server_groups",
                      "used": 10,
                      "quota": 50,
                      "min": 0,
                      "max": -1
                  },
                  {
                      "type": "replications",
                      "used": 1,
                      "quota": 100,
                      "min": 0,
                      "max": -1
                  }
              ]
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

   In this example, **error** represents a general error, including **badrequest** (shown below) and **itemNotFound**.

   .. code-block::

      {
           "badrequest": {
               "message": "XXXX",
               "code": "XXX"
           }
       }

Returned Values
---------------

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
