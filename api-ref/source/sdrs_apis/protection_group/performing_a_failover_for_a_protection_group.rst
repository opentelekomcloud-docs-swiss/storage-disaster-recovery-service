:original_name: sdrs_05_0408.html

.. _sdrs_05_0408:

Performing a Failover for a Protection Group
============================================

Function
--------

When the production site of a protection group becomes faulty, services of the protection group are switched over to the DR site, and servers and disks at the DR site start. After a failover is performed, the current production site of the protection group will become the DR site before the failover. Data synchronization between the production and DR sites will stop. To resume the data synchronization, you need to perform steps provided in :ref:`Enabling Protection or Enabling Protection Again for a Protection Group <sdrs_05_0406>` to enable protection.

Constraints and Limitations
---------------------------

-  The protection group must have replication pairs.
-  **status** of the protection group must be **protected**, **error-failing-over**, or **error-reversing**.
-  If the server at the production site or DR site in a protected instance is deleted using the native interface, no operations can be performed on the protected instance or the protection group of the protected instance.

Constraints on Logging In to the Server After a Planned Failover, Failover, or Disaster Recovery Drill Is Executed First Time Ever
----------------------------------------------------------------------------------------------------------------------------------

After you have performed a planned failover, failover, or DR drill for the first time:

-  If your servers are installed with Cloud-Init/Cloudbase-Init, Cloud-Init/Cloudbase-Init will start along with the server's first startup to inject the initial data. In this case, the password or key pair used to log in to the production site server, disaster recovery site server, or drill server will change.
-  If your servers are not installed with Cloud-Init/Cloudbase-Init, the password or key pair used to log in to the production site server, disaster recovery site server, or drill server will not change.

The following uses a planned failover or failover as the example operation. For the login constraints on drill servers, see those for disaster recovery site servers.

In the following example, Server A and server B are deployed. :ref:`Table 1 <sdrs_05_0408__en-us_topic_0110981899_table92017496206>` shows the servers before and after the operation.

.. _sdrs_05_0408__en-us_topic_0110981899_table92017496206:

.. table:: **Table 1** Servers before and after a planned failover or failover

   ====== ====================== =============================
   ``-``  Production Site Server Disaster Recovery Site Server
   ====== ====================== =============================
   Before Server A               Server B
   After  Server B               Server A
   ====== ====================== =============================

Detailed login constraints are described as follows:

**Scenario 1**: Server A runs Windows and does not have Cloudbase-Init installed. After the first time planned failover or failover:

-  If your servers use password for login, you can use the password of Server A to log in to the production site server (Server B) or disaster recovery site server (Server A).
-  If your servers use key pair for login, you can use the obtained password of Server A to log in to the production site server (Server B) or disaster recovery site server (Server A).

.. note::

   After the first time planned failover or failover, the password or key pair remains the same for the subsequent planned failovers or failovers. In this example:

   You can use the password of Server A to log in to the production site server or disaster recovery site server.

**Scenario 2**: Server A runs Windows and already has Cloudbase-Init installed. After the first time planned failover or failover:

-  When your servers use password for login,

   If Cloudbase-Init is not started (normally within 3 to 5 minutes after the production site server starts), you can use the password of Server B for login.

   After Cloudbase-Init is started, the login password of Server B becomes invalid. Reset the password and use the new password for login.

-  When your servers use key pair for login,

   If Cloudbase-Init is not started (normally within 3 to 5 minutes after the production site server starts), you can use the obtained login password of Server B for login.

   After Cloudbase-Init is started, the obtained login password of Server B becomes invalid. Obtain the password again.

.. note::

   After the first time planned failover or failover, the password or key pair remains the same for the subsequent planned failovers or failovers. In this example:

   -  Login using a password: Reset the password of Server B and use the new password for login.
   -  Login using a key pair: Obtain the password of Server B again and use the obtained password to log in to Server B.

**Scenario 3**: Server A runs Linux. After the first time planned failover or failover:

-  If your servers use password for login, you can use the password of Server A to log in to the production site server (Server B) or disaster recovery site server (Server A). Specifically:

   If the login password of Server A is not changed before the operation, use this password for login.

   If the login password of server A has been changed before the operation, use the new password for login.

   .. note::

      For ECS OSs other than CoreOS, the login password does not change after the first time planned failover or failover.

      For ECSs running CoreOS, the login password of Server A will restore to the initial one after the first time planned failover or failover. In this case, use the login password configured when Server A is created to log in to production site Server A or disaster recovery site Server B.

-  If your server uses key pair for login, use the SSH key pair of Server A to log in to production site Server B or disaster recovery site Server A.

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

   +-----------------------+-----------------+-----------------+---------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                 |
   +=======================+=================+=================+=============================================+
   | failover-server-group | Yes             | Object          | Performs a failover for a protection group. |
   |                       |                 |                 |                                             |
   |                       |                 |                 | This parameter is left empty by default.    |
   +-----------------------+-----------------+-----------------+---------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/server-groups/40df180b-9fe2-471a-8c64-1b758dc84189/action

   .. code-block::

      {
          "failover-server-group": {}
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
