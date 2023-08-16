:original_name: sdrs_05_0512.html

.. _sdrs_05_0512:

Batch Deleting Protected Instances
==================================

Function
--------

This API is used to batch delete protected instances.

Constraints and Limitations
---------------------------

-  **status** of the protected instance must be **available**, **protected**, **failed-over**, **error**, **error-starting**, **error-stopping**, **error-reversing**, **error-failing-over**, **error-deleting**, **error-reprotecting**, **error-resizing**, **invalid**, or **fault**.
-  Protected instances are from the same protection group.
-  If a shared replication pair is attached to multiple protected instances, ensure that all the protected instances with the shared replication pair attached are in the deletion list if you want to delete them in batches.

URI
---

-  URI format

   POST /v1/{project_id}/protected-instances/delete

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

Request
-------

-  Parameter description

   +----------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------+
   | Parameter            | Mandatory       | Type             | Description                                                                                                          |
   +======================+=================+==================+======================================================================================================================+
   | protected_instances  | Yes             | Array of objects | Specifies the protected instances to be deleted. For details, see :ref:`Table 1 <sdrs_05_0512__table1238917531382>`. |
   |                      |                 |                  |                                                                                                                      |
   |                      |                 |                  | .. note::                                                                                                            |
   |                      |                 |                  |                                                                                                                      |
   |                      |                 |                  |    -  A maximum of 20 protected instances are supported by default.                                                  |
   +----------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------+
   | delete_target_server | No              | Boolean          | Specifies whether to delete the DR site server. The default value is **false**.                                      |
   +----------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------+
   | delete_target_eip    | No              | Boolean          | Specifies whether to delete the EIP of the DR site server. The default value is **false**.                           |
   +----------------------+-----------------+------------------+----------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0512__table1238917531382:

   .. table:: **Table 1** Data structure of the **protected_instance** field

      +-----------------+-----------------+-----------------+----------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                          |
      +=================+=================+=================+======================================================================+
      | id              | Yes             | String          | Specifies the ID of a protected instance.                            |
      |                 |                 |                 |                                                                      |
      |                 |                 |                 | For details, see :ref:`Querying Protected Instances <sdrs_05_0503>`. |
      +-----------------+-----------------+-----------------+----------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/protected-instances/delete

   .. code-block::

      {
          "protected_instances": [
                        {
                            "id": "127842d5-f98e-451e-963e-9fb464fbb911"
                        },
                        {
                             "id": "8f5dd226-6cc0-4fe8-9786-b8b3359b234b"
                        }
                     ],
         "delete_target_server": false,
         "delete_target_eip": false
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
         "job_id": "0000000062db92d70162db3ab00f00df"
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
