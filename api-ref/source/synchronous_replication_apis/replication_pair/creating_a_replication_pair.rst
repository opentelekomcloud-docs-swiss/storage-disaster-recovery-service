:original_name: sdrs_05_0601.html

.. _sdrs_05_0601:

Creating a Replication Pair
===========================

Function
--------

This API is used to create a replication pair and add it to the specified protection group.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available** or **protected**.
-  If **server_type** of the protection group is set to **ECS**, the disk status is **Available**.

URI
---

-  URI format

   POST /v1/{project_id}/replications

-  Parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                       |
   +=================+=================+=================+===================================================================================================+
   | project_id      | Yes             | String          | Specifies the project ID.                                                                         |
   |                 |                 |                 |                                                                                                   |
   |                 |                 |                 | For details about how to obtain the project ID, see :ref:`Obtaining a Project ID <sdrs_06_0001>`. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------+

Request
-------

-  Parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                         |
   +=================+=================+=================+=====================================================================+
   | replication     | Yes             | Object          | Specifies the information about a replication pair.                 |
   |                 |                 |                 |                                                                     |
   |                 |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0601__table1282085653515>`. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------+

   .. _sdrs_05_0601__table1282085653515:

   .. table:: **Table 1** **replication** field description

      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                          |
      +=================+=================+=================+======================================================================================================================================================================================================================+
      | server_group_id | Yes             | String          | Specifies the ID of a protection group.                                                                                                                                                                              |
      |                 |                 |                 |                                                                                                                                                                                                                      |
      |                 |                 |                 | You can obtain this value by calling the API described in :ref:`Querying Protection Groups <sdrs_05_0402>`.                                                                                                          |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | volume_id       | Yes             | String          | Specifies the ID of the production site disk.                                                                                                                                                                        |
      |                 |                 |                 |                                                                                                                                                                                                                      |
      |                 |                 |                 | .. note::                                                                                                                                                                                                            |
      |                 |                 |                 |                                                                                                                                                                                                                      |
      |                 |                 |                 |    When the API is successfully invoked, the DR site disk will be automatically created.                                                                                                                             |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name            | Yes             | String          | Specifies the name of a replication pair. The name can contain a maximum of 64 bytes. The value can contain only letters (a to z and A to Z), digits (0 to 9), decimal points (.), underscores (_), and hyphens (-). |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | description     | No              | String          | Specifies the description of a replication pair. The value can contain a maximum of 64 bytes and cannot contain the left angle bracket (<) or right angle bracket (>).                                               |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | cluster_id      | No              | String          | Specifies the DSS storage pool ID.                                                                                                                                                                                   |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/replications

   .. code-block::

      {
          "replication": {
             "server_group_id": "c79fba33-b165-4c69-80c1-d7e590691162",
             "volume_id": "b6f71149-7b9c-4f36-8ff0-1c4809a6f2c2",
             "name": "replication_name",
             "description": "replication_description"
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
