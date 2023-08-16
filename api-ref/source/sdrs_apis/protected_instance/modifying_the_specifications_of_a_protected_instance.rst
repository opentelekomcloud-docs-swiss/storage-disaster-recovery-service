:original_name: sdrs_05_0510.html

.. _sdrs_05_0510:

Modifying the Specifications of a Protected Instance
====================================================

Function
--------

This API is used to modify the specifications of a server in a protected instance, including:

-  Modify the specifications of both the production and DR site servers.
-  Modify the specifications of only the production site server.
-  Modify the specifications of only the DR site server.

You can perform this operation only when the servers of which the specifications to be modified are stopped.

.. note::

   Servers of different specifications have different performance, which may affect applications running on the servers. To ensure the server performance after a planned failover or failover, you are recommended to use servers of specifications (CPU and memory) same or higher than the specifications of the production site servers at the DR site.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available** or **protected**.
-  **status** of the protected instance must be **available**, **protected**, or **error-resizing**.
-  Servers of which the specifications to be modified are stopped.

URI
---

-  URI format

   POST /v1/{project_id}/protected-instances/{protected_instance_id}/resize

-  Parameter description

   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                                                                                   |
   +=======================+=================+=================+===============================================================================================================+
   | project_id            | Yes             | String          | Specifies the project ID.                                                                                     |
   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | protected_instance_id | Yes             | String          | Specifies the ID of a protected instance.                                                                     |
   |                       |                 |                 |                                                                                                               |
   |                       |                 |                 | You can obtain this value by calling the API described in :ref:`Querying Protected Instances <sdrs_05_0503>`. |
   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+

Request
-------

-  Parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                         |
   +=================+=================+=================+=====================================================================+
   | resize          | Yes             | Object          | Modifies the specifications of a protected instance.                |
   |                 |                 |                 |                                                                     |
   |                 |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0510__table0953028102515>`. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------+

   .. _sdrs_05_0510__table0953028102515:

   .. table:: **Table 1** **resize** field description

      +----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter            | Mandatory       | Type            | Description                                                                                                                                                                                                             |
      +======================+=================+=================+=========================================================================================================================================================================================================================+
      | flavorRef            | No              | String          | Specifies the flavor ID of the production and DR site servers after the modification.                                                                                                                                   |
      |                      |                 |                 |                                                                                                                                                                                                                         |
      |                      |                 |                 | .. note::                                                                                                                                                                                                               |
      |                      |                 |                 |                                                                                                                                                                                                                         |
      |                      |                 |                 |    If you specify this parameter, the system modifies the specifications of both the production and DR site servers. After the modification, the production site server and DR site server use the same specifications. |
      +----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | production_flavorRef | No              | String          | Specifies the flavor ID of the production site server after the modification.                                                                                                                                           |
      |                      |                 |                 |                                                                                                                                                                                                                         |
      |                      |                 |                 | .. note::                                                                                                                                                                                                               |
      |                      |                 |                 |                                                                                                                                                                                                                         |
      |                      |                 |                 |    -  If you specify this parameter, the system modifies the specifications of only the production site server.                                                                                                         |
      |                      |                 |                 |    -  If **flavorRef** is specified, **production_flavorRef** does not take effect.                                                                                                                                     |
      +----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | dr_flavorRef         | No              | String          | Specifies the flavor ID of the DR site server after the modification.                                                                                                                                                   |
      |                      |                 |                 |                                                                                                                                                                                                                         |
      |                      |                 |                 | .. note::                                                                                                                                                                                                               |
      |                      |                 |                 |                                                                                                                                                                                                                         |
      |                      |                 |                 |    -  If you specify this parameter, the system modifies the specifications of only the DR site server.                                                                                                                 |
      |                      |                 |                 |    -  If **flavorRef** is specified, **dr_flavorRef** does not take effect.                                                                                                                                             |
      +----------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/protected-instances/00000000632302f501632305f63c000e/resize

   Example 1: Modify the specifications of the production and DR site servers to e2.small. Example request:

   .. code-block::

      {
            "resize": {
                 "flavorRef": "e2.small"
             }
       }

   Example 2: Modify the specifications of the production and DR site serves to s3.small.1 and s3.large.2 respectively. Example request:

   .. code-block::

      {
            "resize": {
                 "production_flavorRef": "s3.small.1",
                 "dr_flavorRef": "s3.large.2"
             }
       }

   Example 3: Modify the specifications of the production site server to e2.small, and retain the DR site server specifications. Example request:

   .. code-block::

      {
            "resize": {
                 "production_flavorRef": "e2.small"
             }
       }

   Example 4: Modify the specifications of the DR site server to e2.small, and retain the production site server specifications. Example request:

   .. code-block::

      {
            "resize": {
                 "dr_flavorRef": "e2.small"
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
          "job_id": "0000000011db92d70162db9d20df32ch"
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
