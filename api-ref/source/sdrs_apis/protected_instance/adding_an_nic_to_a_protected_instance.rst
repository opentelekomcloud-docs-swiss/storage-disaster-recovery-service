:original_name: sdrs_05_0508.html

.. _sdrs_05_0508:

Adding an NIC to a Protected Instance
=====================================

Function
--------

This API is used to add an NIC to the specified protected instance.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available** or **protected**.
-  **status** of the protected instance must be **available** or **protected**.
-  The subnet of the NIC to be added must belong to the same VPC of the protected group and protected instance.

URI
---

-  URI format

   POST /v1/{project_id}/protected-instances/{protected_instance_id}/nic

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

   +-----------------+-----------------+------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type             | Description                                                                                                                                |
   +=================+=================+==================+============================================================================================================================================+
   | subnet_id       | Yes             | String           | Specifies the subnet ID of the NIC to be added. It is **network_id** of the subnet, which is the same as the **neutron_network_id** value. |
   +-----------------+-----------------+------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | security_groups | No              | Array of objects | Specifies the security group of the NIC to be added. Specifies the security group of the NIC.                                              |
   |                 |                 |                  |                                                                                                                                            |
   |                 |                 |                  | For details, see :ref:`Table 1 <sdrs_05_0508__table6280148104910>`.                                                                        |
   +-----------------+-----------------+------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
   | ip_address      | No              | String           | Specifies an IP address. If this parameter is not included, an IP address is automatically assigned.                                       |
   +-----------------+-----------------+------------------+--------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0508__table6280148104910:

   .. table:: **Table 1** **security_groups** field description

      ========= ========= ====== =====================================
      Parameter Mandatory Type   Description
      ========= ========= ====== =====================================
      id        Yes       String Specifies the ID of a security group.
      ========= ========= ====== =====================================

-  Example request

   POST https://{Endpoint}/v1/{project_id}/protected-instances/00000000632302f501632305f63c000e/nic

   .. code-block::

      {

                  "subnet_id": "d32019d3-bc6e-4319-9c1d-6722fc136a23",
                  "security_groups": [
                      {
                          "id": "f0ac4394-7e4a-4409-9701-ba8be283dbc3"
                      }
                  ],
                  "ip_address": "192.168.97.25",

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
         "job_id": "0000000062db92d70162db9d200f32dh"
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
