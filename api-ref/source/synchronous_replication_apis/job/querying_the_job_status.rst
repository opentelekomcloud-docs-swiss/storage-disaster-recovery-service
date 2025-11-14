:original_name: sdrs_05_0101.html

.. _sdrs_05_0101:

Querying the Job Status
=======================

.. _sdrs_05_0101__en-us_topic_0079693002_section34649765:

Function
--------

This API is used to query the execution status of a job.

.. note::

   After a job, such as creating or deleting a protection group, creating or deleting a protected instance, and creating or deleting a replication pair, is issued, **job_id** is returned, based on which you can query the execution status of the job.

URI
---

-  URI format

   GET /v1/{project_id}/jobs/{job_id}

-  Parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                               |
   +=================+=================+=================+===========================================================================================================================================================================================+
   | project_id      | Yes             | String          | Specifies the project ID.                                                                                                                                                                 |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_id          | Yes             | String          | Specifies the job ID.                                                                                                                                                                     |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | Specifies the returned parameter when the asynchronous API command is issued. For details, see the description in :ref:`Function <sdrs_05_0101__en-us_topic_0079693002_section34649765>`. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{endpoint}/v1/{project_id}/jobs/0000000062db92d70162db9d200f000a

Response
--------

-  Parameter description

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                |
   +=======================+=======================+============================================================================================================================================================================================================================+
   | status                | String                | Specifies the job status.                                                                                                                                                                                                  |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | -  **SUCCESS**: The job was successfully executed.                                                                                                                                                                         |
   |                       |                       | -  **RUNNING**: The job is in progress.                                                                                                                                                                                    |
   |                       |                       | -  **FAIL**: The job failed.                                                                                                                                                                                               |
   |                       |                       | -  **INIT**: The job is being initialized.                                                                                                                                                                                 |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | entities              | Object                | Specifies the job object.                                                                                                                                                                                                  |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | The value of this parameter varies depending on the job type. If the job is a protection group-related operation, the value will be **server_group_id**. If a subjob is available, details about the subjob are displayed. |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0101__table503353570>`.                                                                                                                                                            |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_id                | String                | Specifies the job ID.                                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | For details, see the description in :ref:`Function <sdrs_05_0101__en-us_topic_0079693002_section34649765>`.                                                                                                                |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_type              | String                | Specifies the job type.                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | -  **createProtectionGroupNoCG**: Creates a protection group.                                                                                                                                                              |
   |                       |                       | -  **deleteProtectionGroupNoCG**: Deletes a protection group.                                                                                                                                                              |
   |                       |                       | -  **startProtectionGroupNoCG**: Enables protection for a protection group.                                                                                                                                                |
   |                       |                       | -  **reprotectProtectionGroupNoCG**: Enables protection again for a protection group.                                                                                                                                      |
   |                       |                       | -  **stopProtectionGroupNoCG**: Disables protection for a protection group.                                                                                                                                                |
   |                       |                       | -  **failoverProtectionGroupNoCG**: Performs a failover for a protection group.                                                                                                                                            |
   |                       |                       | -  **reverseProtectionGroupNoCG**: Performs a planned failover for a protection group.                                                                                                                                     |
   |                       |                       | -  **createProtectedInstanceNoCG**: Creates a protected instance.                                                                                                                                                          |
   |                       |                       | -  **deleteProtectedInstanceNoCG**: Deletes a protected instance.                                                                                                                                                          |
   |                       |                       | -  **attachReplicationPairNew**: Attaches a replication pair to a protected instance.                                                                                                                                      |
   |                       |                       | -  **detachReplicationPairNew**: Detaches a replication pair from a protected instance.                                                                                                                                    |
   |                       |                       | -  **addNicNew**: Adds a NIC to a protected instance.                                                                                                                                                                      |
   |                       |                       | -  **deleteNicNew**: Deletes a NIC from a protected instance.                                                                                                                                                              |
   |                       |                       | -  **resizeProtectedInstanceNew**: Modifies the specifications of a protected instance.                                                                                                                                    |
   |                       |                       | -  **createReplicationPairNoCG**: Creates a replication pair.                                                                                                                                                              |
   |                       |                       | -  **deleteReplicationPairNoCG**: Deletes a replication pair.                                                                                                                                                              |
   |                       |                       | -  **expandReplicationPairNew**: Expands the capacity of a replication pair.                                                                                                                                               |
   |                       |                       | -  **createDisasterRecoveryDrill**: Creates a DR drill.                                                                                                                                                                    |
   |                       |                       | -  **deleteDisasterRecoveryDrill**: Deletes a DR drill.                                                                                                                                                                    |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | begin_time            | String                | Specifies the start time.                                                                                                                                                                                                  |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | The default format is as follows: "yyyy-MM-dd 'T' HH:mm:ss.SSSZ", for example, **2019-04-01T12:00:00.000Z**.                                                                                                               |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end_time              | String                | Specifies the end time.                                                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | The default format is as follows: "yyyy-MM-dd 'T' HH:mm:ss.SSSZ", for example, **2019-04-01T12:00:00.000Z**.                                                                                                               |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | error_code            | String                | Specifies the error code returned upon a job execution failure.                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | For details, see :ref:`Error Codes <en-us_topic_0113127626>`.                                                                                                                                                              |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | fail_reason           | String                | Specifies the cause of a job execution failure.                                                                                                                                                                            |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | For details, see :ref:`Error Codes <en-us_topic_0113127626>`.                                                                                                                                                              |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | message               | String                | Specifies the error message returned when an error occurs.                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | For details, see the abnormal returned values in :ref:`Returned Values <sdrs_05_0101__en-us_topic_0079693002_section60507121>`.                                                                                            |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | code                  | String                | Specifies the error code returned when an error occurs.                                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                                                                            |
   |                       |                       | For details, see the abnormal returned values in :ref:`Returned Values <sdrs_05_0101__en-us_topic_0079693002_section60507121>`.                                                                                            |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0101__table503353570:

   .. table:: **Table 1** **entities** field description

      +-----------------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Type             | Description                                                                                                                                                                           |
      +=================+==================+=======================================================================================================================================================================================+
      | server_group_id | String           | Specifies the ID of the protection group being queried.                                                                                                                               |
      +-----------------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | sub_jobs        | Array of objects | Specifies the execution information of a subjob. When no subjob exists, the value of this parameter is left empty. The structure of each subjob is similar to that of the parent job. |
      +-----------------+------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
            "status": "SUCCESS",
            "entities": {
                "server_group_id": "a59d008e-4bad-4bf3-9b17-6cc25e7da483"
            },
            "job_id": "0000000062db92d70162db9d200f000a",
            "job_type": "createProtectionGroupNoCG",
            "begin_time": "2018-04-19T01:55:30.443Z",
            "end_time": "2018-04-19T01:55:45.493Z",
            "error_code": null,
            "fail_reason": null
        }

   Or

   .. code-block::

      {
          "job_id": "ff8080826b45d4a5016b5036242c0025",
          "job_type": "stopProtectionGroupNoCG",
          "begin_time": "2019-06-13T09:40:53.930Z",
          "end_time": "2019-06-13T09:41:01.946Z",
          "status": "SUCCESS",
          "error_code": null,
          "fail_reason": null,
          "entities": {
              "sub_jobs": [
                  {
                      "job_id": "ff8080826b45d4a5016b50362868002a",
                      "job_type": "stopProtectionGroupRepNoCG",
                      "begin_time": "2019-06-13T09:40:55.015Z",
                      "end_time": "2019-06-13T09:40:58.951Z",
                      "status": "SUCCESS",
                      "error_code": null,
                      "fail_reason": null,
                      "entities": {
                          "server_group_id": "1fd6903c-48f9-4772-8974-112dfbd74427"
                      }
                  },
                  {
                      "job_id": "ff8080826b45d4a5016b50362870002b",
                      "job_type": "stopProtectionGroupRepNoCG",
                      "begin_time": "2019-06-13T09:40:55.022Z",
                      "end_time": "2019-06-13T09:40:58.952Z",
                      "status": "SUCCESS",
                      "error_code": null,
                      "fail_reason": null,
                      "entities": {
                          "server_group_id": "1fd6903c-48f9-4772-8974-112dfbd74427"
                      }
                  }
              ]
          }
      }
      {
           "error": {
               "message": "XXXX",
               "code": "XXX"
           }
       }

.. _sdrs_05_0101__en-us_topic_0079693002_section60507121:

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
