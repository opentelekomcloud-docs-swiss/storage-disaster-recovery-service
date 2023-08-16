:original_name: sdrs_05_0401.html

.. _sdrs_05_0401:

Creating a Protection Group
===========================

Function
--------

This API is used to create a protection group.

.. note::

   This API is an asynchronous interface. If this API is invoked successfully, the request is issued. To query the creation result, invoke the API described in :ref:`Querying the Job Status <sdrs_05_0101>`.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   POST /v1/{project_id}/server-groups

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

Request
-------

-  Parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                         |
   +=================+=================+=================+=====================================================================+
   | server_group    | Yes             | Object          | Specifies the information about a protection group.                 |
   |                 |                 |                 |                                                                     |
   |                 |                 |                 | For details, see :ref:`Table 1 <sdrs_05_0401__table5487195132418>`. |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------+

   .. _sdrs_05_0401__table5487195132418:

   .. table:: **Table 1** **server_group** field description

      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                | Mandatory       | Type            | Description                                                                                                                                                                                                          |
      +==========================+=================+=================+======================================================================================================================================================================================================================+
      | name                     | Yes             | String          | Specifies the name of a protection group. The name can contain a maximum of 64 bytes. The value can contain only letters (a to z and A to Z), digits (0 to 9), decimal points (.), underscores (_), and hyphens (-). |
      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | description              | No              | String          | Specifies the description of a protection group. The description can contain a maximum of 64 bytes. The value cannot contain the left angle bracket (<) or right angle bracket (>).                                  |
      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | source_availability_zone | Yes             | String          | Specifies the production site AZ of a protection group.                                                                                                                                                              |
      |                          |                 |                 |                                                                                                                                                                                                                      |
      |                          |                 |                 | You can obtain this value by calling the API described in :ref:`Active-Active Domain <sdrs_05_0300>`.                                                                                                                |
      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | target_availability_zone | Yes             | String          | Specifies the DR site AZ of a protection group.                                                                                                                                                                      |
      |                          |                 |                 |                                                                                                                                                                                                                      |
      |                          |                 |                 | You can obtain this value by calling the API described in :ref:`Active-Active Domain <sdrs_05_0300>`.                                                                                                                |
      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | domain_id                | Yes             | String          | Specifies the ID of an active-active domain.                                                                                                                                                                         |
      |                          |                 |                 |                                                                                                                                                                                                                      |
      |                          |                 |                 | You can obtain this value by calling the API described in :ref:`Active-Active Domain <sdrs_05_0300>`.                                                                                                                |
      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | source_vpc_id            | Yes             | String          | Specifies the ID of the VPC for the production site.                                                                                                                                                                 |
      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | dr_type                  | No              | String          | Specifies the deployment model. The default value is **migration**, indicating migration within a VPC.                                                                                                               |
      +--------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example request

   POST https://{endpoint}/v1/{project_id}/server-groups

   .. code-block::

      {
          "server_group":
          {
              "name":"testname",
              "description":"description",
              "source_availability_zone":"AZ01",
              "target_availability_zone":"AZ02",
              "domain_id":"fb4bb8e3-a574-4437-a156-78c916aeea4d",
              "source_vpc_id":"046852ef-c49d-409b-8389-546aaaa5701f",
              "dr_type":"migration",
                      "server_type":"ECS"
          }
      }

Response
--------

-  Parameter description

   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                   |
   +=======================+=======================+===============================================================================================================================================================================================================+
   | job_id                | String                | Specifies the job ID.                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                               |
   |                       |                       | Specifies the returned parameter when the asynchronous API command is issued successfully. For details about the task execution result, see the description in :ref:`Querying the Job Status <sdrs_05_0101>`. |
   +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
         "job_id": "0000000062db92d70162db9d200f000a"
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
