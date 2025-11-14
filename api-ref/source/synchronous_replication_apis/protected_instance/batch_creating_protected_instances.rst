:original_name: sdrs_05_0511.html

.. _sdrs_05_0511:

Batch Creating Protected Instances
==================================

Function
--------

This API is used to batch create protected instances. When a protected instance is created, the default name of the server at the DR site is the same as that of the server at the production site, but their IDs are different. To modify a server name, click the server name on the protected instance details page to switch to the server details page and modify the server name. Alternatively, you can call the API in :ref:`Changing the Name of a Protected Instance <sdrs_05_0505>` to modify the name.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available** or **protected**.
-  If you want to use a server with a shared disk attached to create a protected instance, ensure that all the servers with the shared disk attached are in the creation list if you want to create the protected instances in batches.
-  No protected instance has been created using the server.
-  The server must be in the same VPC as the protection group.
-  If protection is enabled for servers created during capacity expansion of an AS group, these servers cannot be deleted when the capacity of the AS group is reduced.
-  If the server at the production site runs Windows and you choose the key login mode, ensure that the key pair of the server exists when you create a protected instance. Otherwise, the server at the DR site may fail to create, causing the protected instance creation failure.

   .. note::

      If the key pair of the production site server has been deleted, create a key pair with the same name.

-  After you create a protected instance and enable protection on servers at the production site, modifications to the **Hostname**, **Name**, **Security Group**, **Agency**, **ECS Group**, **Tags**, and **Auto Recovery** configurations of servers on the production site will not synchronize to the servers at the DR site. You can manually add the configuration items to the servers at the DR site on the management console.

URI
---

-  URI format

   POST /v1/{project_id}/protected-instances/batch

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

Request
-------

-  Parameter description

   +---------------------+-----------------+-----------------+---------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                         |
   +=====================+=================+=================+=====================================================================+
   | protected_instances | Yes             | Object          | Specifies the information about a protected instance.               |
   |                     |                 |                 |                                                                     |
   |                     |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0511__table1632215113348>`. |
   +---------------------+-----------------+-----------------+---------------------------------------------------------------------+

   .. _sdrs_05_0511__table1632215113348:

   .. table:: **Table 1** **protected_instances** field description

      +-------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter         | Mandatory       | Type             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                  |
      +===================+=================+==================+==============================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | name_prefix       | Yes             | String           | Specifies the prefix of a protected instance name. When you create protected instances in batches, the system will automatically add a suffix to each protected instance name prefix to differentiate the protected instances, such as "-0001". Each protected instance name prefix can contain 1 to 59 characters, and consists of only letters (a to z and A to Z), digits (0 to 9), decimal points (.), underscores (_), and hyphens (-). |
      +-------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | description       | No              | String           | Specifies the description of protected instances. The description can contain a maximum of 64 characters. The value cannot contain the left angle bracket (<) or right angle bracket (>).                                                                                                                                                                                                                                                    |
      +-------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | server_group_id   | Yes             | String           | Specifies the ID of the protection group where the protected instances are added.                                                                                                                                                                                                                                                                                                                                                            |
      |                   |                 |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
      |                   |                 |                  | For details, see :ref:`Querying Protection Groups <sdrs_05_0402>`.                                                                                                                                                                                                                                                                                                                                                                           |
      +-------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | primary_subnet_id | No              | String           | Specifies the subnet ID of the primary NIC on the DR site server. The value is the same as that of **neutron_network_id**.                                                                                                                                                                                                                                                                                                                   |
      +-------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | servers           | Yes             | Array of objects | Specifies the servers for creating protected instances.                                                                                                                                                                                                                                                                                                                                                                                      |
      |                   |                 |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
      |                   |                 |                  | For details, see :ref:`Table 2 <sdrs_05_0511__table18611665512>`.                                                                                                                                                                                                                                                                                                                                                                            |
      |                   |                 |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
      |                   |                 |                  | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                    |
      |                   |                 |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                              |
      |                   |                 |                  |    A maximum of five servers are supported by default.                                                                                                                                                                                                                                                                                                                                                                                       |
      +-------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0511__table18611665512:

   .. table:: **Table 2** Data structure of the **server_info** field

      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                    |
      +=================+=================+=================+================================================================================================================================================================================================================================================================================================================================================================+
      | server_id       | Yes             | String          | Specifies the ID of the production site server.                                                                                                                                                                                                                                                                                                                |
      |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                 |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                      |
      |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                 |                 |                 |    When the API is successfully invoked, the DR site server will be automatically created.                                                                                                                                                                                                                                                                     |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | flavorRef       | No              | String          | Specifies the flavor ID of the DR site server.                                                                                                                                                                                                                                                                                                                 |
      |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                 |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                      |
      |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                |
      |                 |                 |                 |    -  If this parameter is not specified, the flavor ID of the DR site server is the same as that of the production site server by default.                                                                                                                                                                                                                    |
      |                 |                 |                 |    -  Servers of different specifications have different performance, which may affect applications running on the servers. To ensure the server performance after a planned failover or failover, you are recommended to use servers of specifications (CPU and memory) same or higher than the specifications of the production site servers at the DR site. |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/protected-instances/batch

   .. code-block::

      {
               "protected_instances":{
                     "name_prefix": "test_protected_instance_name",
                     "description": "my description",
                     "server_group_id": "523ab8ad-3759-4933-9436-4cf4ebb20867",
                     "primary_subnet_id": "a32217fh-3413-c313-6342-3124d3491502",
                     "servers": [
                        {
                            "server_id": "403b603d-1d91-42cc-a357-81f3c2daf43f",
                            "flavorRef":"c3.medium.2"
                        },
                        {
                             "server_id": "8f5dd226-6cc0-4fe8-9786-b8b3359b234b"
                        }
                     ],
                     "tenancy": "dedicated",
                     "dedicated_host_id": "0bc41598-1b5a-4bd2-872a-82e6abb82e68",
                     "tags": [
                        {
                            "key": "test",
                            "value":"aaaaa"
                        }
                     ],
               }
        }

Response
--------

-  Parameter description

   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                                                                                               |
   +===========+========+===========================================================================================================================================================================================================+
   | job_id    | String | This is a returned parameter when the asynchronous API command is issued successfully. For details about the task execution result, see the description in :ref:`Querying the Job Status <sdrs_05_0101>`. |
   +-----------+--------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

**Returned Value**
------------------

-  Normal

   ============== ====================================
   Returned Value Description
   ============== ====================================
   202            The server has accepted the request.
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
