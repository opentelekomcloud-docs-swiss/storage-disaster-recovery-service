:original_name: sdrs_05_0503.html

.. _sdrs_05_0503:

Querying Protected Instances
============================

Function
--------

This API is used to query all protected instances of the current tenant.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/protected-instances

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

-  **Request filter** field description

   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Mandatory       | Type             | Description                                                                                                                                                                                                             |
   +========================+=================+==================+=========================================================================================================================================================================================================================+
   | server_group_id        | No              | String           | Specifies the ID of the protection group, in which all protected instances are queried.                                                                                                                                 |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | For details, see the parameter description in :ref:`Querying Protection Groups <sdrs_05_0402>`.                                                                                                                         |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | server_group_ids       | No              | Array of strings | Specifies the protection group ID list. The value is in the following format: server_group_ids=['server_group_id1','server_group_id2',...,'server_group_idx']. Convert it using URL encoding.                           |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | -  All the protected instances with valid **server_group_id** in **server_group_ids** are returned.                                                                                                                     |
   |                        |                 |                  | -  The protected instances of a maximum of 30 **server_group_id** values can be queried.                                                                                                                                |
   |                        |                 |                  | -  If parameters **server_group_id** and **server_group_ids** are both specified in the request, **server_group_id** will be ignored.                                                                                   |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | protected_instance_ids | No              | Array of strings | Specifies the protected instance ID list. The value is in the following format: protected_instance_ids=['protected_instance_id1','protected_instance_id2',...,'protected_instance_idx']. Convert it using URL encoding. |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | -  All the protected instances with valid **protected_instance_id** in **protected_instance_ids** are returned.                                                                                                         |
   |                        |                 |                  | -  The protected instances of a maximum of 30 **protected_instance_id** values can be queried.                                                                                                                          |
   |                        |                 |                  | -  If parameter **server_group_id** or **server_group_ids** is specified in the request, **protected_instance_ids** will be ignored.                                                                                    |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | limit                  | No              | Integer          | Specifies the maximum number of results returned each time. The value is a positive integer from 0 to 1000. The default value is **1000**.                                                                              |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | offset                 | No              | Integer          | Specifies the offset of each request. The default value is **0**. The value must be a positive integer and cannot be negative.                                                                                          |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                 | No              | String           | Specifies the status of a protected instance.                                                                                                                                                                           |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | For details, see :ref:`Protected Instance Status <en-us_topic_0126152931>`.                                                                                                                                             |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name                   | No              | String           | Specifies the name of a protected instance. Fuzzy search is supported.                                                                                                                                                  |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | query_type             | No              | String           | Specifies the query type.                                                                                                                                                                                               |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | -  **status_abnormal**: indicates to query protected instances in the abnormal status.                                                                                                                                  |
   |                        |                 |                  | -  This parameter is invalid when the value is set to **general** or left empty.                                                                                                                                        |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | availability_zone      | No              | String           | Specifies the current production site AZ of the protection group containing the protected instance.                                                                                                                     |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | You can obtain this value by calling the API described in :ref:`Querying an Active-Active Domain <sdrs_05_0301>`.                                                                                                       |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Request parameter description

   None

-  Example request

   .. code-block:: text

      GET https://{Endpoint}/v1/{project_id}/protected-instances?server_group_ids=%5b%2221d65fa4-430e-4761-b9ad-4e27364f874c%22%2c%22943c7d15-0371-4b89-b1a6-db1ef35c9263%22%5d&status=available

   .. note::

      Use URL encoding for **server_group_ids** or **protected_instance_ids**.

Response
--------

-  Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                     |
   +=======================+=======================+=================================================================+
   | protected_instances   | Array of objects      | Specifies the information about protected instances.            |
   |                       |                       |                                                                 |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0503__table503353570>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | count                 | Integer               | Specifies the number of protected instances.                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------+

   .. _sdrs_05_0503__table503353570:

   .. table:: **Table 1** **protected_instances** field description

      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                             |
      +=======================+=======================+=========================================================================================================+
      | id                    | String                | Specifies the ID of a protected instance.                                                               |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | name                  | String                | Specifies the name of a protected instance.                                                             |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | description           | String                | Specifies the description of a protected instance.                                                      |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | server_group_id       | String                | Specifies the ID of a protection group.                                                                 |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | status                | String                | Specifies the status of a protected instance.                                                           |
      |                       |                       |                                                                                                         |
      |                       |                       | For details, see :ref:`Protected Instance Status <en-us_topic_0126152931>`.                             |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | progress              | Integer               | Specifies the synchronization progress of a protected instance.                                         |
      |                       |                       |                                                                                                         |
      |                       |                       | Unit: %                                                                                                 |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | source_server         | String                | Specifies the production site server ID.                                                                |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | target_server         | String                | Specifies the DR site server ID.                                                                        |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | created_at            | String                | Specifies the time when a protected instance was created.                                               |
      |                       |                       |                                                                                                         |
      |                       |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**.  |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | updated_at            | String                | Specifies the time when a protected instance was updated.                                               |
      |                       |                       |                                                                                                         |
      |                       |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**.  |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | priority_station      | String                | Specifies the current production site AZ of the protection group containing the protected instance.     |
      |                       |                       |                                                                                                         |
      |                       |                       | -  **source**: indicates that the current production site AZ is the **source_availability_zone** value. |
      |                       |                       | -  **target**: indicates that the current production site AZ is the **target_availability_zone** value. |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | attachment            | Array of objects      | Specifies the attached replication pairs.                                                               |
      |                       |                       |                                                                                                         |
      |                       |                       | For details, see :ref:`Table 2 <sdrs_05_0503__table1575342962014>`.                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | tags                  | Array of objects      | Specifies the tag list.                                                                                 |
      |                       |                       |                                                                                                         |
      |                       |                       | For details, see :ref:`Table 3 <sdrs_05_0503__table12339146338>`.                                       |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+
      | metadata              | Object                | Specifies the metadata of a protected instance.                                                         |
      |                       |                       |                                                                                                         |
      |                       |                       | For details, see :ref:`Table 4 <sdrs_05_0503__table8582730112710>`.                                     |
      +-----------------------+-----------------------+---------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0503__table1575342962014:

   .. table:: **Table 2** **attachment** field description

      =========== ====== =======================================
      Parameter   Type   Description
      =========== ====== =======================================
      replication String Specifies the ID of a replication pair.
      device      String Specifies the device name.
      =========== ====== =======================================

   .. _sdrs_05_0503__table12339146338:

   .. table:: **Table 3** **tags** field description

      ========= ====== ========================
      Parameter Type   Description
      ========= ====== ========================
      key       String Specifies the tag key.
      value     String Specifies the tag value.
      ========= ====== ========================

   .. _sdrs_05_0503__table8582730112710:

   .. table:: **Table 4** Field **metadata** description

      +-----------------------+-----------------------+------------------------------------------------------+
      | Parameter             | Type                  | Description                                          |
      +=======================+=======================+======================================================+
      | \__system__frozen     | String                | Specifies whether the resource is frozen.            |
      |                       |                       |                                                      |
      |                       |                       | -  **true**: indicates that the resource is frozen.  |
      |                       |                       | -  Empty: indicates that the resource is not frozen. |
      +-----------------------+-----------------------+------------------------------------------------------+

-  Example response

   .. code-block::

      {
          "protected_instances": [
              {
                  "id": "67a2cc7e-fb87-41a8-ba28-9c032abcaee1",
                  "name": "protected_instance_xff",
                  "description": "protected_instance_xff",
                  "server_group_id": "21d65fa4-430e-4761-b9ad-4e27364f874c",
                  "status": "available",
                  "progress": 0,
                  "source_server": "d1e8e8a7-ae6f-4f40-bead-20093976961e",
                  "target_server": "9bad52b9-ca5a-4274-ba9e-3c8ca9843fa1",
                  "created_at": "2018-11-06 11:09:25.861",
                  "updated_at": "2018-11-06 11:12:11.716",
                  "priority_station": "source",
                  "attachment": [
                      {
                          "replication": "08d6b5a0-9a12-4263-a468-30d71d10498c",
                          "device": "/dev/vdb"
                      },
                      {
                          "replication": "4c332757-dc77-458d-9883-03d701cde2f2",
                          "device": "/dev/vda"
                      }
                  ],
                  "tags": [
                      {
                         "key": "aaaaaaa",
                         "value": "01234567889"
                       },
                      {
                          "key": "ffffff",
                          "value": "dddd"
                      }
                  ],
                  "metadata": {}
              },
              {
                  "id": "50f5091e-9e9e-473c-a932-2a2cbcbeb1ff",
                  "name": "ecs_sdrs_test",
                  "description": "1111",
                  "server_group_id": "943c7d15-0371-4b89-b1a6-db1ef35c9263",
                  "status": "protected",
                  "progress": 100,
                  "source_server": "5fb92d6c-b0cb-46c9-824b-b90ec5500ae6",
                  "target_server": "c6c0ff54-fa1f-43ef-9ccc-1774e40c8745",
                  "created_at": "2018-11-06 09:27:52.258",
                  "updated_at": "2018-11-06 09:44:59.853",
                  "priority_station": "target",
                  "attachment": [
                      {
                          "replication": "6568f7c4-0510-4f39-929d-8ffccbd4fd47",
                          "device": "/dev/vda"
                      }
                  ],
                  "tags": [
                      {
                           "key": "aaaaaaa",
                           "value": "01234567889"
                      },
                      {
                           "key": "ffffff",
                           "value": "dddd"                }
                  ],
                  "metadata": {}
              }
          ],
          "count": 2
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
