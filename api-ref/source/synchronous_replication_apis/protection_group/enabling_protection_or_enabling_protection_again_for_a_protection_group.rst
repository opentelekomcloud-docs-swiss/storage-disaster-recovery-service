:original_name: sdrs_05_0406.html

.. _sdrs_05_0406:

Enabling Protection or Enabling Protection Again for a Protection Group
=======================================================================

Function
--------

This API is used to enable protection or enable protection again for a protection group.

Constraints and Limitations (Enabling Protection)
-------------------------------------------------

-  The protection group must have replication pairs.
-  **status** of the protection group must be **available** or **error-starting**.
-  After you create a protected instance and enable protection on servers at the production site, modifications to the **Hostname**, **Name**, **Security Group**, **Agency**, **ECS Group**, **Tags**, and **Auto Recovery** configurations of servers on the production site will not synchronize to the servers at the DR site. You can manually add the configuration items to the servers at the DR site on the management console.

Constraints and Limitations (Enabling Protection Again)
-------------------------------------------------------

-  **status** of the protection group must be **failed-over** or **error-reprotecting**.
-  Before you enable the protection again, ensure that the servers at the DR site are stopped.

URI
---

-  URI format

   POST /v1/{project_id}/server-groups/{server_group_id}/action

-  Parameter description

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                        |
   +=================+=================+=================+====================================================================+
   | project_id      | Yes             | String          | Specifies the project ID.                                          |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------+
   | server_group_id | Yes             | String          | Specifies the ID of a protection group.                            |
   |                 |                 |                 |                                                                    |
   |                 |                 |                 | For details, see :ref:`Querying Protection Groups <sdrs_05_0402>`. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------+

Request
-------

-  Parameter description

   +--------------------+-----------------+-----------------+--------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                |
   +====================+=================+=================+============================================+
   | start-server-group | Yes             | Object          | Enables protection for a protection group. |
   |                    |                 |                 |                                            |
   |                    |                 |                 | This parameter is left empty.              |
   +--------------------+-----------------+-----------------+--------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/server-groups/40df180b-9fe2-471a-8c64-1b758dc84189/action

   .. code-block::

      {
          "start-server-group": {}
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
          "job_id": "ff8080826adfae02016ae2d123fc05ed"
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
