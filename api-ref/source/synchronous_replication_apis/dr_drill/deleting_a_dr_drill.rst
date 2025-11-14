:original_name: sdrs_05_0702.html

.. _sdrs_05_0702:

Deleting a DR Drill
===================

Function
--------

This API is used to delete a specified DR drill. After you delete the specified DR drill:

-  The DR drill as well as the disks and NICs attached to the DR drill will be deleted.
-  The drill VPC and subnets of the drill VPC will not be deleted. You can create other servers using this VPC.

Constraints and Limitations
---------------------------

The status of the DR drill must be **available**, **error**, or **error-deleting**.

URI
---

-  URI format

   DELETE /v1/{project_id}/disaster-recovery-drills/{disaster_recovery_drill_id}

-  Parameter description

   +----------------------------+-----------------+-----------------+-----------------------------------------------------------------+
   | Parameter                  | Mandatory       | Type            | Description                                                     |
   +============================+=================+=================+=================================================================+
   | project_id                 | Yes             | String          | Specifies the project ID.                                       |
   +----------------------------+-----------------+-----------------+-----------------------------------------------------------------+
   | disaster_recovery_drill_id | Yes             | String          | Specifies the DR drill ID.                                      |
   |                            |                 |                 |                                                                 |
   |                            |                 |                 | To query details, see :ref:`Querying DR Drills <sdrs_05_0703>`. |
   +----------------------------+-----------------+-----------------+-----------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   DELETE https://{Endpoint}/v1/{project_id}/disaster-recovery-drills/f96ac55f-35dd-4cc3-ba61-36c168900c99

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
          "job_id": "0000000011db92d34587db9d20df32ch"
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
