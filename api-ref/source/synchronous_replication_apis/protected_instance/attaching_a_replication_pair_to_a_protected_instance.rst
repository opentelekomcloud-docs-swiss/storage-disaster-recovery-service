:original_name: sdrs_05_0506.html

.. _sdrs_05_0506:

Attaching a Replication Pair to a Protected Instance
====================================================

Function
--------

This API is used to attach the specified replication pair to the specified protected instance.

Constraints and Limitations
---------------------------

-  **status** of the protection group must be **available** or **protected**.
-  **status** of the protected instance must be **available** or **protected**.
-  **status** of the replication pair must be **available** or **protected**.
-  The non-shared replication pair has not been attached to any protected instance.

URI
---

-  URI format

   POST /v1/{project_id}/protected-instances/{protected_instance_id}/attachreplication

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

   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                                         |
   +=======================+=================+=================+=====================================================================+
   | replicationAttachment | Yes             | Object          | Attaches a replication pair to a protected instance.                |
   |                       |                 |                 |                                                                     |
   |                       |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0506__table1470881204413>`. |
   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------+

   .. _sdrs_05_0506__table1470881204413:

   .. table:: **Table 1** **replicationAttachment** field description

      +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                               |
      +=================+=================+=================+===========================================================================================================================================================================================================================================================================================================================================================================================================================================+
      | replication_id  | Yes             | String          | Specifies the ID of a replication pair.                                                                                                                                                                                                                                                                                                                                                                                                   |
      |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                           |
      |                 |                 |                 | You can obtain this value by calling the API described in :ref:`Querying Replication Pairs <sdrs_05_0603>`.                                                                                                                                                                                                                                                                                                                               |
      +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | device          | Yes             | String          | Specifies the disk device name of a replication pair.                                                                                                                                                                                                                                                                                                                                                                                     |
      |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                           |
      |                 |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                 |
      |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                           |
      |                 |                 |                 |    -  The new disk device name cannot be the same as an existing one.                                                                                                                                                                                                                                                                                                                                                                     |
      |                 |                 |                 |    -  Set the parameter value to **/dev/sda** for the system disks of protected instances created using Xen servers and to **/dev/sd**\ *x* for data disks, where *x* is a letter in alphabetical order. For example, if there are two data disks, set the device names of the two data disks to **/dev/sdb** and **/dev/sdc**, respectively. If you set a device name starting with **/dev/vd**, the system uses **/dev/sd** by default. |
      |                 |                 |                 |    -  Set the parameter value to **/dev/vda** for the system disks of protected instances created using KVM servers and to **/dev/vd**\ *x* for data disks, where *x* is a letter in alphabetical order. For example, if there are two data disks, set the device names of the two data disks to **/dev/vdb** and **/dev/vdc**, respectively. If you set a device name starting with **/dev/sd**, the system uses **/dev/vd** by default. |
      +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/protected-instances/00000000632302f501632305f63c000e/attachreplication

   .. code-block::

      {
           "replicationAttachment": {
              "replication_id": "6568f7c4-0510-4f39-929d-8ffccbd4fd47",
              "device": "/dev/vda"
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
