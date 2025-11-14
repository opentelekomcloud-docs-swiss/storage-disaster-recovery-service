:original_name: sdrs_05_0301.html

.. _sdrs_05_0301:

Querying an Active-Active Domain
================================

Function
--------

This API is used to query an active-active domain.

An active-active domain consists of the local storage device and remote storage device. Application servers can access data across data centers using an active-active domain.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/active-domains

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

Request
-------

-  Example request

   GET https://{Endpoint}/v1/{project_id}/active-domains

Response
--------

-  Parameter description

   +-----------------------+-----------------------+--------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                        |
   +=======================+=======================+====================================================================+
   | domains               | Array of objects      | Specifies the information about an active-active domain.           |
   |                       |                       |                                                                    |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0301__table155991608555>`. |
   +-----------------------+-----------------------+--------------------------------------------------------------------+

   .. _sdrs_05_0301__table155991608555:

   .. table:: **Table 1** **domains** field description

      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                  | Type                  | Description                                                                                                                                        |
      +============================+=======================+====================================================================================================================================================+
      | id                         | String                | Specifies the ID of an active-active domain.                                                                                                       |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
      | name                       | String                | Specifies the name of an active-active domain.                                                                                                     |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
      | description                | String                | Specifies the description of an active-active domain.                                                                                              |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
      | sold_out                   | Boolean               | Specifies whether resources of an active-active domain are sold out.                                                                               |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
      | local_replication_cluster  | Object                | Specifies the parameters related to the replication cluster in one AZ (either the production site AZ or DR site AZ) of the active-active domain.   |
      |                            |                       |                                                                                                                                                    |
      |                            |                       | For details, see :ref:`Table 2 <sdrs_05_0301__table503353570>`.                                                                                    |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+
      | remote_replication_cluster | Object                | Specifies the parameters related to replication cluster in the other AZ (either the production site AZ or DR site AZ) of the active-active domain. |
      |                            |                       |                                                                                                                                                    |
      |                            |                       | For details, see :ref:`Table 3 <sdrs_05_0301__table1166111616216>`.                                                                                |
      +----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0301__table503353570:

   .. table:: **Table 2** **local_replication_cluster** field description

      ================= ====== ============================
      Parameter         Type   Description
      ================= ====== ============================
      availability_zone String Specifies the name of an AZ.
      ================= ====== ============================

   .. _sdrs_05_0301__table1166111616216:

   .. table:: **Table 3** **remote_replication_cluster** field description

      ================= ====== ============================
      Parameter         Type   Description
      ================= ====== ============================
      availability_zone String Specifies the name of an AZ.
      ================= ====== ============================

-  Example response

   .. code-block::

      {
          "domains": [
              {
                  "id": "fb4bb8e3-a574-4437-a156-78c916aeea4d",
                  "name": "ActiveactiveDomain",
                  "description": "my domain",
                  "sold_out": false,
                  "local_replication_cluster": {
                      "availability_zone": "AZ01"
                  },
                  "remote_replication_cluster": {
                      "availability_zone": "AZ02"
                  }
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
