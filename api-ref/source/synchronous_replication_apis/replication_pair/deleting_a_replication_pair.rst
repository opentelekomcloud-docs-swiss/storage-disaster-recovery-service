:original_name: sdrs_05_0602.html

.. _sdrs_05_0602:

Deleting a Replication Pair
===========================

Function
--------

This API is used to delete a specified replication pair.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available**, **protected**, **failed-over**, **error-starting**, **error-stopping**, **error-reversing**, or **error-failing-over**, **error-deleting**, or **error-reprotecting**.
-  **status** of the replication pair must be **available**, **protected**, **failed-over**, **error**, **error-starting**, **error-stopping**, **error-reversing**, **error-failing-over**, **error-deleting**, **error-reprotecting**, **error-attaching**, **error-extending**, **invalid**, or **fault**.
-  The replication pair has not been attached to a protected instance.

URI
---

-  URI format

   DELETE /v1/{project_id}/replications/{replication_id}

-  Parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                 |
   +=================+=================+=================+=============================================================================================================+
   | project_id      | Yes             | String          | Specifies the project ID.                                                                                   |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | replication_id  | Yes             | String          | Specifies the ID of a replication pair.                                                                     |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | You can obtain this value by calling the API described in :ref:`Querying Replication Pairs <sdrs_05_0603>`. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+

Request
-------

-  Parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                       |
   +=================+=================+=================+===================================================================+
   | replication     | Yes             | Object          | Specifies the information about a replication pair.               |
   |                 |                 |                 |                                                                   |
   |                 |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0602__table38261646898>`. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------+

   .. _sdrs_05_0602__table38261646898:

   .. table:: **Table 1** **replication** field description

      +----------------------+-----------+---------+-------------------------------------------------------------------------------+
      | Parameter            | Mandatory | Type    | Description                                                                   |
      +======================+===========+=========+===============================================================================+
      | server_group_id      | No        | String  | Specifies the ID of a protection group.                                       |
      +----------------------+-----------+---------+-------------------------------------------------------------------------------+
      | delete_target_volume | No        | Boolean | Specifies whether to delete the DR site disk. The default value is **false**. |
      +----------------------+-----------+---------+-------------------------------------------------------------------------------+

-  Example request

   DELETE https://{Endpoint}/v1/{project_id}/replications/b93bc1c4-67ee-45a1-bc8a-d022fdd28811

   .. code-block::

      {
         "replication": {
             "server_group_id": "c79fba33-b165-4c69-80c1-d7e590691162",
              "delete_target_volume": false
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
