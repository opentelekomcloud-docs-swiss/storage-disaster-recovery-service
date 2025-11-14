:original_name: sdrs_05_0507.html

.. _sdrs_05_0507:

Detaching a Replication Pair from a Protected Instance
======================================================

Function
--------

This API is used to detach a specified replication pair from a specified protected instance.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available**, **protected**, **failed-over**, **error-starting**, **error-stopping**, **error-reversing**, or **error-failing-over**.
-  **status** of the protected instance must be **available**, **protected**, **failed-over**, **error-starting**, **error-stopping**, **error-reversing**, **error-failing-over**, **error-deleting**, **error-reprotecting**, **error-resizing**, **invalid**, or **fault**.
-  **status** of the replication pair must be **available**, **protected**, **failed-over**, **error-attaching**, **error-detaching**, **error-starting**, **error-stopping**, **error-reversing**, **error-failing-over**, **error-deleting**, **error-reprotecting**, **error-extending**, **invalid**, or **fault**.
-  The replication pair has been attached to a protected instance.

.. note::

   -  A system disk (attached to **/dev/sda** or **/dev/vda**) can be detached only when the server is in the **Stopped** state. Therefore, stop the server before detaching the system disk.
   -  Data disks can be detached online or offline, which means that the server containing the disks can either be in the **Running** or **Stopped** state.

URI
---

-  URI format

   DELETE /v1/{project_id}/protected-instances/{protected_instance_id}/detachreplication/{replication_id}

-  Parameter description

   +-----------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                                                                                                                          |
   +=======================+=================+=================+======================================================================================================================================================+
   | project_id            | Yes             | String          | Specifies the project ID.                                                                                                                            |
   +-----------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | protected_instance_id | Yes             | String          | Specifies the ID of a protected instance.                                                                                                            |
   |                       |                 |                 |                                                                                                                                                      |
   |                       |                 |                 | You can obtain this value by calling the API described in :ref:`Querying Protected Instances <sdrs_05_0503>`.                                        |
   +-----------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | replication_id        | Yes             | String          | Specifies the ID of a replication pair.                                                                                                              |
   |                       |                 |                 |                                                                                                                                                      |
   |                       |                 |                 | You can query replication pairs attached to the protected instance by calling the API described in :ref:`Querying Replication Pairs <sdrs_05_0603>`. |
   +-----------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   DELETE http://{Endpoint}/v1/{project_id}/protected-instances/00000000632302f501632305f63c000e/detachreplication/6568f7c4-0510-4f39-929d-8ffccbd4fd47

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
         "job_id": "0000000062db92d70162db921dgf00bb"
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
