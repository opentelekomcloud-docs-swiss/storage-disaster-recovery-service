:original_name: sdrs_05_0409.html

.. _sdrs_05_0409:

Performing a Planned Failover for a Protection Group
====================================================

Function
--------

When you perform a planned failover for a protection group, the current production site of the protection group is switched to the DR site specified when the protection group is created, or reverse. After the planned failover is performed, data synchronization between the production site and DR site continues, but the direction is reverse.

Constraints and Limitations
---------------------------

-  The protection group must have replication pairs.
-  **status** of the protection group must be **protected** or **error-reversing**.
-  All servers at the current production site of the protection group are stopped. During a planned failover, do not start servers at the production site and DR site. Otherwise, the planned failover may fail.
-  If the production site server or DR site server of a protected instance is deleted using the native interface, the planned failover or planned failback will fail, and the protected instance as well as the protection group will become unavailable.

Restrictions on Logging In to a Server After You Perform a Planned Failover for the First Time
----------------------------------------------------------------------------------------------

-  If the production site server (when the protected instance is created) runs Windows and has Cloudbase-Init installed, pay attention to the following restrictions after you perform a planned failover for the first time:

   -  If you choose to use a password for the server login, you can use the password of the production site server 3 to 5 minutes after the DR site server starts and before Cloudbase-Init starts. It takes 1 to 2 minutes for the server to display the login UI.

      After Cloudbase-Init starts, manually reset the password on the DR site server.

      After you perform a planned failback, use the configured password to log in to the production site server.

   -  If you choose to use a key for the server login, you can use the password obtained from the production site server 3 to 5 minutes after the DR site server starts and before Cloudbase-Init starts. It takes 1 to 2 minutes for the server to display the login UI.

      After Cloudbase-Init starts, use the password obtained from the DR site server for the login.

      After you perform a planned failback, use the obtained password to log in to the production site server.

   .. note::

      If you change the login password of the DR site server after you perform a planned failover for the first time, log in to the DR site server using the new password. After you perform a planned failback again, use the new password to log in to the production site server.

-  If the production site server (when the protected instance is created) runs Windows and has no Cloudbase-Init installed, pay attention to the following restrictions after you perform a planned failover or failover for the first time:

   -  If you choose to use a password for the server login, use the password of the production site server to log in to the production site or DR site server.
   -  If you choose to use a key for the server login, use the password obtained from the production site server to log in to the production site or DR site server.

-  If the production site server (when the protected instance is created) runs Linux, pay attention to the following restrictions after you perform a planned failover or failover for the first time:

   -  If you choose to use a password for the server login, use the password of the production site server to log in to the production site or DR site server.

      .. note::

         For servers running CoreOS, if you change the login password of the production site server after you perform a planned failover for the first time, log in to the DR site server using the new password. After you perform a planned failback again, use the initial password to log in to the production site server.

   -  If you choose to use a key for the server login, use the password obtained from the production site server to log in to the production site or DR site server.

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

   +----------------------+-----------------+-----------------+--------------------------------------------------------------------+
   | Parameter            | Mandatory       | Type            | Description                                                        |
   +======================+=================+=================+====================================================================+
   | reverse-server-group | Yes             | Object          | Performs a planned failover for a protection group.                |
   |                      |                 |                 |                                                                    |
   |                      |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0409__table104985554308>`. |
   +----------------------+-----------------+-----------------+--------------------------------------------------------------------+

   .. _sdrs_05_0409__table104985554308:

   .. table:: **Table 1** **reverse-server-group** field description

      +------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter        | Mandatory       | Type            | Description                                                                                                                                                                    |
      +==================+=================+=================+================================================================================================================================================================================+
      | priority_station | Yes             | String          | Specifies the direction of the planned failover.                                                                                                                               |
      |                  |                 |                 |                                                                                                                                                                                |
      |                  |                 |                 | -  **target**: indicates to fail services from the production site specified when the protection group is created to the DR site specified when a protection group is created. |
      |                  |                 |                 | -  **source**: indicates to fail services from the DR site specified when the protection group is created to the production site specified when a protection group is created. |
      +------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/server-groups/40df180b-9fe2-471a-8c64-1b758dc84189/action

   .. code-block::

      {
        "reverse-server-group": {
          "priority_station": "source"
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
         "job_id": "0000000062db92d70162db9d200f002d"
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
