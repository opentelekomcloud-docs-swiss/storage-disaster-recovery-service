:original_name: sdrs_05_0901.html

.. _sdrs_05_0901:

Querying Failed Tasks
=====================

Function
--------

This API is used to query failed tasks of all protection groups or failed tasks in a specified protection group.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/task-center/failure-jobs

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

-  **Request filter** field description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                 |
   +=================+=================+=================+=============================================================================================+
   | failure_status  | No              | String          | Query the task failure status.                                                              |
   |                 |                 |                 |                                                                                             |
   |                 |                 |                 | -  **createFail**: indicates a creation failure.                                            |
   |                 |                 |                 | -  **deleteFail**: indicates a deletion failure.                                            |
   |                 |                 |                 | -  **attachFail**: indicates an attachment failure.                                         |
   |                 |                 |                 | -  **detachFail**: indicates a detachment failure.                                          |
   |                 |                 |                 | -  **expandFail**: indicates an expansion failure.                                          |
   |                 |                 |                 | -  **resizeFail**: indicates a specification change failure.                                |
   |                 |                 |                 | -  **startFail**: indicates a protection enabling failure.                                  |
   |                 |                 |                 | -  **stopFail**: indicates a protection disabling failure.                                  |
   |                 |                 |                 | -  **reverseFail**: indicates a planned failover failure.                                   |
   |                 |                 |                 | -  **failoverFail**: indicates a failover failure.                                          |
   |                 |                 |                 | -  **reprotectFail**: indicates a re-protection enabling failure.                           |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------+
   | resource_name   | No              | String          | Specifies the resource name of a protection group.                                          |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------+
   | server_group_id | No              | String          | Specifies the ID of a protection group.                                                     |
   |                 |                 |                 |                                                                                             |
   |                 |                 |                 | For details, see :ref:`Querying Protection Groups <sdrs_05_0402>`.                          |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------+
   | resource_type   | No              | String          | Specifies the resource type.                                                                |
   |                 |                 |                 |                                                                                             |
   |                 |                 |                 | -  **server_groups**: indicates a protection group.                                         |
   |                 |                 |                 | -  **protected_instances**: indicates a protected instance.                                 |
   |                 |                 |                 | -  **replications**: indicates a replication pair.                                          |
   |                 |                 |                 | -  **disaster_recovery_drills**: indicates a DR drill.                                      |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------+
   | limit           | No              | Integer         | Specifies the maximum number of results returned each time.                                 |
   |                 |                 |                 |                                                                                             |
   |                 |                 |                 | The value is a positive integer ranging from **0** to **1000**, and is **1000** by default. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------+
   | offset          | No              | Integer         | Specifies the offset of each request. The default value is **0**.                           |
   |                 |                 |                 |                                                                                             |
   |                 |                 |                 | The value must be a number and cannot be negative.                                          |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{Endpoint}/v1/{project_id}/task-center/failure-jobs

   GET https://{Endpoint}/v1/{project_id}/task-center/failure-jobs?server_group_id=XXXXX

   .. note::

      -  If you do not specify **filter** in the request, the system displays failed tasks of the protection group level, such as failed protection group creation or deletion tasks.
      -  To query failed tasks in a protection group, specify **server_group_id** in **filter**.

Response
--------

-  Parameter description

   +-----------------------+-----------------------+--------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                        |
   +=======================+=======================+====================================================================+
   | failure_jobs          | list                  | Specifies the list of the failed tasks.                            |
   |                       |                       |                                                                    |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0901__table687013217358>`. |
   +-----------------------+-----------------------+--------------------------------------------------------------------+
   | count                 | Integer               | Specifies the number of failed tasks in the list.                  |
   +-----------------------+-----------------------+--------------------------------------------------------------------+

   .. _sdrs_05_0901__table687013217358:

   .. table:: **Table 1** **failure_jobs** field description

      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                                                                                                                               |
      +=======================+=======================+===========================================================================================================================================================================================================+
      | job_status            | String                | Specifies the task status.                                                                                                                                                                                |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | The value can be **FAIL** only in current version.                                                                                                                                                        |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | -  **FAIL**: The task failed.                                                                                                                                                                             |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | resource_id           | String                | Specifies the resource ID.                                                                                                                                                                                |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | resource_name         | String                | Specifies the resource name.                                                                                                                                                                              |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | resource_type         | String                | Specifies the resource type.                                                                                                                                                                              |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | -  **server_groups**: indicates a protection group.                                                                                                                                                       |
      |                       |                       | -  **protected_instances**: indicates a protected instance.                                                                                                                                               |
      |                       |                       | -  **replications**: indicates a replication pair.                                                                                                                                                        |
      |                       |                       | -  **disaster_recovery_drills**: indicates a DR drill.                                                                                                                                                    |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | failure_status        | String                | Specifies the failed task status.                                                                                                                                                                         |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | -  **createFail**: indicates a creation failure.                                                                                                                                                          |
      |                       |                       | -  **deleteFail**: indicates a deletion failure.                                                                                                                                                          |
      |                       |                       | -  **attachFail**: indicates an attachment failure.                                                                                                                                                       |
      |                       |                       | -  **detachFail**: indicates a detachment failure.                                                                                                                                                        |
      |                       |                       | -  **expandFail**: indicates an expansion failure.                                                                                                                                                        |
      |                       |                       | -  **resizeFail**: indicates a specification change failure.                                                                                                                                              |
      |                       |                       | -  **startFail**: indicates a protection enabling failure.                                                                                                                                                |
      |                       |                       | -  **stopFail**: indicates a protection disabling failure.                                                                                                                                                |
      |                       |                       | -  **reverseFail**: indicates a planned failover failure.                                                                                                                                                 |
      |                       |                       | -  **failoverFail**: indicates a failover failure.                                                                                                                                                        |
      |                       |                       | -  **reprotectFail**: indicates a re-protection enabling failure.                                                                                                                                         |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | job_id                | String                | Specifies the task ID.                                                                                                                                                                                    |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | This is a returned parameter when the asynchronous API command is issued successfully. For details about the task execution result, see the description in :ref:`Querying the Job Status <sdrs_05_0101>`. |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | job_type              | String                | Specifies the task name.                                                                                                                                                                                  |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | begin_time            | String                | Specifies the task operation time.                                                                                                                                                                        |
      |                       |                       |                                                                                                                                                                                                           |
      |                       |                       | The default format is as follows: "yyyy-MM-ddTHH:mm:ss.SSSZ", for example, **2019-04-01T12:00:00.000Z**.                                                                                                  |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | error_code            | String                | Specifies the error code for a failed task.                                                                                                                                                               |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | fail_reason           | String                | Specifies the task failure cause.                                                                                                                                                                         |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
          "count": 2,
          "failure_jobs": [
              {
                  "job_status": "FAIL",
                  "resource_id": "17984002-ad8a-438b-8ba6-b850224634c5",
                  "resource_name": "Protected-Instance-ab14",
                  "resource_type": "protectedInstance",
                  "failure_status": "createFail",
                  "job_id": "ff808082686f229a0168707beaab014e",
                  "job_type": "createProtectedInstance",
                  "begin_time": "2019-01-21T12:56:35.754Z",
                  "error_code": "EVS.2024",
                  "fail_reason": "SdrsGenerateNativeServerParamsTask-fail:volume is error!"
              },
              {
                  "job_status": "FAIL",
                  "resource_id": "897f57b2-6e94-4179-b414-9532726c59f2",
                  "resource_name": "Protected-Instance-5e2e",
                  "resource_type": "protectedInstance",
                  "failure_status": "createFail",
                  "job_id": "ff808082686f229a0168707b9be9013e",
                  "job_type": "createProtectedInstance",
                  "begin_time": "2019-01-21T12:56:15.591Z",
                  "error_code": "EVS.2024",
                  "fail_reason": "SdrsGenerateNativeServerParamsTask-fail:volume is error!"
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
