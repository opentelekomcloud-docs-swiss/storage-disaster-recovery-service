:original_name: sdrs_05_0605.html

.. _sdrs_05_0605:

Expanding the Capacity of a Replication Pair
============================================

Function
--------

This API is used to expand the capacity of the two disks in a replication pair.

Constraints and Limitations
---------------------------

-  **status** of the replication pair must be **available**, **protected**, or **error-extending**.
-  **status** of disks in the replication pair is **available** or **in-use**.

.. note::

   -  When the disks in a replication pair are not shared

      If the disks in the replication pair are in the **in-use** state, the replication pair capacity can be expanded only when online capacity expansion is supported.

   -  When the disks in a replication pair are shared

      The replication pair capacity cannot be expanded online if the disks are in the **in-use** state.

URI
---

-  URI format

   POST /v1/{project_id}/replications/{replication_id}/action

-  Parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                 |
   +=================+=================+=================+=============================================================================================================+
   | project_id      | Yes             | String          | Specifies the project ID.                                                                                   |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | replication_id  | Yes             | String          | Specifies the ID of a replication pair.                                                                     |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | You can obtain this value by calling the API described in :ref:`Querying Replication Pairs <sdrs_05_0603>`. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+

Request
-------

-  Parameter description

   +--------------------+-----------------+-----------------+--------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                                        |
   +====================+=================+=================+====================================================================+
   | extend-replication | Yes             | Object          | Expands disk capacity.                                             |
   |                    |                 |                 |                                                                    |
   |                    |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0605__table931745011362>`. |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------+

   .. _sdrs_05_0605__table931745011362:

   .. table:: **Table 1** **extend-replication** field description

      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+
      | Parameter       | Mandatory       | Type            | Description                                                                                            |
      +=================+=================+=================+========================================================================================================+
      | new_size        | Yes             | Integer         | Specifies the disk capacity after expansion in a replication pair.                                     |
      |                 |                 |                 |                                                                                                        |
      |                 |                 |                 | Unit: GB                                                                                               |
      |                 |                 |                 |                                                                                                        |
      |                 |                 |                 | .. note::                                                                                              |
      |                 |                 |                 |                                                                                                        |
      |                 |                 |                 |    If the value has a decimal point, the system takes the integer before the decimal point by default. |
      +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{Endpoint}/v1/{project_id}/replications/b93bc1c4-67ee-45a1-bc8a-d022fdd28811/action

   .. code-block::

      {
          "extend-replication": {
              "new_size": 10
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
         "job_id": "0000000011db92d34587db9d20df32ch"
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
