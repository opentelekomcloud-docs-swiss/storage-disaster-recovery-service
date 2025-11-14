:original_name: sdrs_05_0701.html

.. _sdrs_05_0701:

Creating a DR Drill
===================

Function
--------

This API is used to create a disaster recovery (DR) drill.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available**, **protected**, **failed-over**, **error-starting**, **error-stopping**, **error-reversing**, **error-reprotecting**, or **error-failing-over**.
-  Do not perform a DR drill before the first time data synchronization completes. Otherwise, the drill server may not start properly.
-  If **drill_vpc_id** is specified (the system uses an existing drill VPC), the drill VPC CIDR block must be consistent with that of the VPC for the protection group. If **drill_vpc_id** is not specified, the system automatically creates a drill VPC.
-  When you use a created drill VPC to create a drill, the subnet ACL rule of the drill VPC will be different from that of the VPC of the protection group. You need to manually set them to be the same one if needed.
-  When you create a DR drill, if the VPC of the protection group has a customized routing table and subnets configured, the corresponding routing table will not be automatically created for the drill VPC. You need to manually create it if needed.

URI
---

-  URI format

   POST /v1/{project_id}/disaster-recovery-drills

-  Parameter description

========== ========= ====== =========================
Parameter  Mandatory Type   Description
========== ========= ====== =========================
project_id Yes       String Specifies the project ID.
========== ========= ====== =========================

Request
-------

-  Parameter description

   +-------------------------+-----------------+-----------------+--------------------------------------------------------------------+
   | Parameter               | Mandatory       | Type            | Description                                                        |
   +=========================+=================+=================+====================================================================+
   | disaster_recovery_drill | Yes             | Object          | Specifies the information about a DR drill.                        |
   |                         |                 |                 |                                                                    |
   |                         |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0701__table592231164010>`. |
   +-------------------------+-----------------+-----------------+--------------------------------------------------------------------+

   .. _sdrs_05_0701__table592231164010:

   .. table:: **Table 1** **disaster_recovery_drill** field description

      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                  |
      +=================+=================+=================+==============================================================================================================================================================================================================+
      | server_group_id | Yes             | String          | Specifies the ID of a protection group.                                                                                                                                                                      |
      |                 |                 |                 |                                                                                                                                                                                                              |
      |                 |                 |                 | For details, see :ref:`Querying Protection Groups <sdrs_05_0402>`.                                                                                                                                           |
      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | drill_vpc_id    | No              | String          | Specifies the drill VPC ID. If you do not specify this parameter, the system will automatically create a drill VPC.                                                                                          |
      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name            | Yes             | String          | Specifies the name of a DR drill. The name can contain a maximum of 64 bytes. The value can contain only letters (a to z and A to Z), digits (0 to 9), decimal points (.), underscores (_), and hyphens (-). |
      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/disaster-recovery-drills

   .. code-block::

      {
               "disaster_recovery_drill": {
                        "name": "dr_drill_test",
                        "server_group_id":"c2aee29a-2959-4d01-9755-01cc76a4d17d",
                        "drill_vpc_id":"87d505be-e984-455e-ad84-588c73fb258b"
          }
      }

Response
--------

-  Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                               |
   +=======================+=======================+===========================================================================================================================================================================================================+
   | job_id                | String                | Specifies the job ID.                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | This is a returned parameter when the asynchronous API command is issued successfully. For details about the task execution result, see the description in :ref:`Querying the Job Status <sdrs_05_0101>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
          "job_id": "0000000011db92d36662db9d20df32ch"
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
