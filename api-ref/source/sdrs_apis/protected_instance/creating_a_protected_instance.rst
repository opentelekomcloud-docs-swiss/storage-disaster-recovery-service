:original_name: sdrs_05_0501.html

.. _sdrs_05_0501:

Creating a Protected Instance
=============================

Function
--------

This API is used to create a protected instance. When a protected instance is created, the default name of the server at the DR site is the same as that of the server at the production site, but their IDs are different. To modify a server name, click the server name on the protected instance details page to switch to the server details page and modify the server name. Alternatively, you can call the API in :ref:`Changing the Name of a Protected Instance <sdrs_05_0505>` to modify the name.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available** or **protected**.
-  No shared disk has been attached to the server.
-  No protected instance has been created using the server.
-  The server must be in the same VPC as the protection group.
-  If protection is enabled for servers created during capacity expansion of an Auto Scaling (AS) group, these servers cannot be deleted when the capacity of the AS group is reduced.
-  If the server at the production site runs Windows and you choose the key login mode, ensure that the key pair of the server exists when you create a protected instance. Otherwise, the server at the DR site may fail to create, causing the protected instance creation failure.

   .. note::

      If the key pair of the production site server has been deleted, create a key pair with the same name.

-  After you create a protected instance and enable protection on servers at the production site, modifications to the **Hostname**, **Name**, **Security Group**, **Agency**, **ECS Group**, **Tags**, and **Auto Recovery** configurations of servers on the production site will not synchronize to the servers at the DR site. You can manually add the configuration items to the servers at the DR site on the management console.

URI
---

-  URI format

   POST /v1/{project_id}/protected-instances

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

Request
-------

-  Parameter description

   +--------------------+-----------------+-----------------+---------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                                         |
   +====================+=================+=================+=====================================================================+
   | protected_instance | Yes             | Object          | Specifies the information about a protected instance.               |
   |                    |                 |                 |                                                                     |
   |                    |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0501__table1632215113348>`. |
   +--------------------+-----------------+-----------------+---------------------------------------------------------------------+

   .. _sdrs_05_0501__table1632215113348:

   .. table:: **Table 1** **protected_instance** field description

      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter          | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                    |
      +====================+=================+=================+================================================================================================================================================================================================================================================================================================================================================================+
      | server_group_id    | Yes             | String          | Specifies the ID of the protection group where a protected instance is added.                                                                                                                                                                                                                                                                                  |
      |                    |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 | For details, see :ref:`Querying Protection Groups <sdrs_05_0402>`.                                                                                                                                                                                                                                                                                             |
      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | server_id          | Yes             | String          | Specifies the ID of the production site server.                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                      |
      |                    |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 |    When the API is successfully invoked, the DR site server will be automatically created.                                                                                                                                                                                                                                                                     |
      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name               | Yes             | String          | Specifies the name of a protected instance. The name can contain a maximum of 64 bytes. The value can contain only letters (a to z and A to Z), digits (0 to 9), decimal points (.), underscores (_), and hyphens (-).                                                                                                                                         |
      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | description        | No              | String          | Specifies the description of a protected instance. The description can contain a maximum of 64 bytes. The value cannot contain the left angle bracket (<) or right angle bracket (>).                                                                                                                                                                          |
      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | primary_subnet_id  | No              | String          | Specifies the network ID of the subnet for the primary NIC on the DR site server. The value is the same as that of **neutron_network_id** obtained using the VPC API.                                                                                                                                                                                          |
      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | primary_ip_address | No              | String          | Specifies the IP address of the primary NIC on the DR site server.                                                                                                                                                                                                                                                                                             |
      |                    |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 | This parameter is valid only when **primary_subnet_id** is specified.                                                                                                                                                                                                                                                                                          |
      |                    |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 | If this parameter is not specified when **primary_subnet_id** is specified, the system automatically assigns an IP address to the primary NIC on the DR site server                                                                                                                                                                                            |
      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | flavorRef          | No              | String          | Specifies the flavor ID of the DR site server                                                                                                                                                                                                                                                                                                                  |
      |                    |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                      |
      |                    |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                    |                 |                 |    -  If this parameter is not specified, the flavor ID of the DR site server is the same as that of the production site server by default.                                                                                                                                                                                                                    |
      |                    |                 |                 |    -  Servers of different specifications have different performance, which may affect applications running on the servers. To ensure the server performance after a planned failover or failover, you are recommended to use servers of specifications (CPU and memory) same or higher than the specifications of the production site servers at the DR site. |
      +--------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/protected-instances

   .. code-block::

      {
               "protected_instance":{
                     "server_group_id": "523ab8ad-3759-4933-9436-4cf4ebb20867",
                     "server_id": "403b603d-1d91-42cc-a357-81f3c2daf43f",
                     "name": "test_protected_instance_name",
                     "description": "my description",
                     "primary_subnet_id": "a32217fh-3413-c313-6342-3124d3491502",
                     "primary_ip_address": "192.168.0.5",
                     "flavorRef": "s3.large.2",
               }
        }

Response
--------

-  Parameter description

   +-----------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                                                                                                   |
   +===========+========+===============================================================================================================================================================================================================+
   | job_id    | String | Specifies the returned parameter when the asynchronous API command is issued successfully. For details about the task execution result, see the description in :ref:`Querying the Job Status <sdrs_05_0101>`. |
   +-----------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
         "job_id": "0000000062db92d70162db9d200f00bb"
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
