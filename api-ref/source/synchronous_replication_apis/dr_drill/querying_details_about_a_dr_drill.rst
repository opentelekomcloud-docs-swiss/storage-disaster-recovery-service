:original_name: sdrs_05_0704.html

.. _sdrs_05_0704:

Querying Details About a DR Drill
=================================

Function
--------

This API is used to query the details about a DR drill.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/disaster-recovery-drills/{disaster_recovery_drill_id}

-  Parameter description

   +----------------------------+-----------------------+-----------------------------------------------------------------+
   | Parameter                  | Mandatory             | Description                                                     |
   +============================+=======================+=================================================================+
   | project_id                 | Yes                   | Specifies the project ID.                                       |
   +----------------------------+-----------------------+-----------------------------------------------------------------+
   | disaster_recovery_drill_id | Yes                   | Specifies the DR drill ID.                                      |
   |                            |                       |                                                                 |
   |                            |                       | To query details, see :ref:`Querying DR Drills <sdrs_05_0703>`. |
   +----------------------------+-----------------------+-----------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{Endpoint}/v1/{project_id}/disaster-recovery-drills/e472d26f-9624-42fb-8bfc-717d4714c225

Response
--------

-  Parameter description

   +-------------------------+-----------------------+---------------------------------------------------------------------+
   | Parameter               | Type                  | Description                                                         |
   +=========================+=======================+=====================================================================+
   | disaster_recovery_drill | Object                | Specifies the information about a DR drill.                         |
   |                         |                       |                                                                     |
   |                         |                       | For details, see :ref:`Table 1 <sdrs_05_0704__table1540192213355>`. |
   +-------------------------+-----------------------+---------------------------------------------------------------------+

   .. _sdrs_05_0704__table1540192213355:

   .. table:: **Table 1** **disaster_recovery_drill** field description

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                            |
      +=======================+=======================+========================================================================================================+
      | id                    | String                | Specifies the DR drill ID.                                                                             |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | name                  | String                | Specifies the DR drill name.                                                                           |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | status                | String                | Specifies the DR drill status. For details, see :ref:`DR Drill Status <en-us_topic_0126152933>`.       |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | drill_vpc_id          | String                | Specifies the ID of the VPC used for a DR drill.                                                       |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | created_at            | String                | Specifies the time when a DR drill was created.                                                        |
      |                       |                       |                                                                                                        |
      |                       |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**. |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | updated_at            | String                | Specifies the time when a DR drill was updated.                                                        |
      |                       |                       |                                                                                                        |
      |                       |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**. |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | server_group_id       | String                | Specifies the ID of a protection group.                                                                |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+
      | drill_servers         | Array of objects      | Specifies the drill servers.                                                                           |
      |                       |                       |                                                                                                        |
      |                       |                       | For details, see :ref:`Table 2 <sdrs_05_0704__table469122153514>`.                                     |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0704__table469122153514:

   .. table:: **Table 2** **drill_servers** field description

      +--------------------+--------+----------------------------------------------------------+
      | Parameter          | Type   | Description                                              |
      +====================+========+==========================================================+
      | protected_instance | String | Specifies the protected instance ID of the drill server. |
      +--------------------+--------+----------------------------------------------------------+
      | drill_server_id    | String | Specifies the drill server ID.                           |
      +--------------------+--------+----------------------------------------------------------+

-  Example response

   .. code-block::

      {
           "disaster_recovery_drill":
               {
                   "id": "e472d26f-9624-42fb-8bfc-717d4714c225",
                  "name": "dr_drill_test",
                  "status": "available",
                  "server_group_id": "c2aee29a-2959-4d01-9755-01cc76a4d17d",
                  "drill_vpc_id": "7881f1d2-1f41-419c-873a-14ac620bc46e",
                  "created_at": "2018-07-18 06:41:58.681",
                  "updated_at": "2018-07-18 00:41:14.677",
                  "drill_servers": [
                      {
                          "protected_instance": "d08ca8d7-a784-41ae-b32a-c592943f5dfc",
                          "drill_server_id": "9de0439a-4ee4-4199-919a-44afd20952dc"
                      },
                      {
                          "protected_instance": "ea308e8b-043c-4fc6-a53c-856eae137b13",
                          "drill_server_id": "3eaa1c70-9719-4eb5-b577-cb92ddbffd03"
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
