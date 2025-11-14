:original_name: sdrs_05_0603.html

.. _sdrs_05_0603:

Querying Replication Pairs
==========================

Function
--------

This API is used to query all replication pairs in a specified protection group. If you do not specify the protection group, the system lists all the replication pairs of the tenant.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/replications

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
   | server_group_id        | No              | String           | Specifies the ID of a protection group.                                                                                                                                                                                 |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | You can obtain this value by calling the API described in :ref:`Querying Protection Groups <sdrs_05_0402>`.                                                                                                             |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | server_group_ids       | No              | Array of strings | Specifies the protection group ID list. The value is in the following format: server_group_ids=['server_group_id1','server_group_id2',...,'server_group_idx']. Convert it using URL encoding.                           |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | -  All the replication pairs with valid **server_group_id** in **server_group_ids** are returned.                                                                                                                       |
   |                        |                 |                  | -  The replication pairs of a maximum of 30 **server_group_id** values can be queried.                                                                                                                                  |
   |                        |                 |                  | -  If parameters **server_group_id** and **server_group_ids** are both specified in the request, **server_group_id** will be ignored.                                                                                   |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | protected_instance_id  | No              | String           | Specifies the ID of a protected instance.                                                                                                                                                                               |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | You can obtain this value by calling the API described in :ref:`Querying Protected Instances <sdrs_05_0503>`.                                                                                                           |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | protected_instance_ids | No              | Array of strings | Specifies the protected instance ID list. The value is in the following format: protected_instance_ids=['protected_instance_id1','protected_instance_id2',...,'protected_instance_idx']. Convert it using URL encoding. |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | -  All the replication pairs with valid **protected_instance_id** in **protected_instance_ids** are returned.                                                                                                           |
   |                        |                 |                  | -  The replication pairs of a maximum of 30 **protected_instance_id** values can be queried.                                                                                                                            |
   |                        |                 |                  | -  If parameters **protected_instance_id** and **protected_instance_ids** are both specified in the request, **protected_instance_id** will be ignored.                                                                 |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name                   | No              | String           | Specifies the name of a replication pair. Fuzzy search is supported.                                                                                                                                                    |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status                 | No              | String           | Specifies the status of a replication pair.                                                                                                                                                                             |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | For details, see :ref:`Replication Pair Status <en-us_topic_0126152932>`.                                                                                                                                               |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | limit                  | No              | Integer          | Specifies the maximum number of results returned each time. The value is a positive integer from 0 to 1000. The default value is **1000**.                                                                              |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | offset                 | No              | Integer          | Specifies the offset of each request. The default value is **0**. The value must be a number and cannot be negative.                                                                                                    |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | query_type             | No              | String           | Specifies the query type.                                                                                                                                                                                               |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | -  To query replication pairs in the abnormal status, set **query_type** to **status_abnormal**.                                                                                                                        |
   |                        |                 |                  | -  Otherwise, set **query_type** to general or leave it empty.                                                                                                                                                          |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | availability_zone      | No              | String           | Specifies the current production site AZ of the protection group containing the replication pair.                                                                                                                       |
   |                        |                 |                  |                                                                                                                                                                                                                         |
   |                        |                 |                  | You can obtain this value by calling the API described in :ref:`Querying an Active-Active Domain <sdrs_05_0301>`.                                                                                                       |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | volume_id              | No              | String           | Specifies the ID of the disk used to create a replication pair.                                                                                                                                                         |
   +------------------------+-----------------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   .. code-block::

      https://{Endpoint}/v1/{project_id}/replications?server_group_ids=%5b%2221d65fa4-430e-4761-b9ad-4e27364f874c%22%2c%22943c7d15-0371-4b89-b1a6-db1ef35c9263&status=available

   .. note::

      Use URL encoding for **server_group_ids** or **protected_instance_ids**.

Response
--------

-  Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                           |
   +=======================+=======================+=======================================================================+
   | replications          | Array of objects      | Specifies the information about replication pairs.                    |
   |                       |                       |                                                                       |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0603__table111111245194113>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------+
   | count                 | Integer               | Specifies the number of replication pairs.                            |
   +-----------------------+-----------------------+-----------------------------------------------------------------------+

   .. _sdrs_05_0603__table111111245194113:

   .. table:: **Table 1** **replications** field description

      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                                                                                                  |
      +=======================+=======================+==============================================================================================================================================+
      | id                    | String                | Specifies the ID of a replication pair.                                                                                                      |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | name                  | String                | Specifies the name of a replication pair.                                                                                                    |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | description           | String                | Specifies the description of a replication pair.                                                                                             |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_model     | String                | Specifies the replication mode of a replication pair. The default value is **hypermetro**, indicating synchronous replication.               |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | status                | String                | Specifies the status of a replication pair.                                                                                                  |
      |                       |                       |                                                                                                                                              |
      |                       |                       | For details, see :ref:`Replication Pair Status <en-us_topic_0126152932>`.                                                                    |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | progress              | Integer               | Specifies the synchronization progress of a replication pair.                                                                                |
      |                       |                       |                                                                                                                                              |
      |                       |                       | Unit: %                                                                                                                                      |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_status    | String                | Specifies the data synchronization status.                                                                                                   |
      |                       |                       |                                                                                                                                              |
      |                       |                       | -  **active**: Data has been synchronized.                                                                                                   |
      |                       |                       | -  **inactive**: Data is not synchronized.                                                                                                   |
      |                       |                       | -  **copying**: Data is being synchronized.                                                                                                  |
      |                       |                       | -  **active-stopped**: Data synchronization is stopped.                                                                                      |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | attachment            | Array of objects      | Specifies the device name.                                                                                                                   |
      |                       |                       |                                                                                                                                              |
      |                       |                       | For details, see :ref:`Table 2 <sdrs_05_0603__table47791613195012>`.                                                                         |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | server_group_id       | String                | Specifies the ID of a protection group.                                                                                                      |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | volume_ids            | String                | Specifies the ID of the disk used to create a replication pair.                                                                              |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | priority_station      | String                | Specifies the current production site AZ of the protection group containing the replication pair.                                            |
      |                       |                       |                                                                                                                                              |
      |                       |                       | -  **source**: indicates that the current production site AZ is the **source_availability_zone** value.                                      |
      |                       |                       | -  **target**: indicates that the current production site AZ is the **target_availability_zone** value.                                      |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | fault_level           | String                | Specifies the fault level of a replication pair.                                                                                             |
      |                       |                       |                                                                                                                                              |
      |                       |                       | -  **0**: No fault occurs.                                                                                                                   |
      |                       |                       | -  **2**: The disk of the current production site does not have read/write permissions. In this case, you are advised to perform a failover. |
      |                       |                       | -  **5**: The replication link is disconnected. In this case, a failover is not allowed. Contact the administrator.                          |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | created_at            | String                | Specifies the time when a replication pair was created.                                                                                      |
      |                       |                       |                                                                                                                                              |
      |                       |                       | The default format is as follows: ""yyyy-MM-ddTHH:mm:ss.SSSSSS", for example, **2019-04-01T12:00:00.000000**.                                |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | updated_at            | String                | Specifies the time when a replication pair was updated.                                                                                      |
      |                       |                       |                                                                                                                                              |
      |                       |                       | The default format is as follows: ""yyyy-MM-ddTHH:mm:ss.SSSSSS", for example, **2019-04-01T12:00:00.000000**.                                |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | record_metadata       | Object                | Specifies the SDR data of a replication pair.                                                                                                |
      |                       |                       |                                                                                                                                              |
      |                       |                       | For details, see :ref:`Table 3 <sdrs_05_0603__table5781813115015>`.                                                                          |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | failure_detail        | String                | Specifies the error code returned only when **status** of a replication pair is **error**.                                                   |
      |                       |                       |                                                                                                                                              |
      |                       |                       | For details, see the returned value in :ref:`Error Codes <en-us_topic_0113127626>`.                                                          |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0603__table47791613195012:

   .. table:: **Table 2** **attachment** field description

      +--------------------+--------+---------------------------------------------------------------------------------------+
      | Parameter          | Type   | Description                                                                           |
      +====================+========+=======================================================================================+
      | device             | String | Specifies the device name.                                                            |
      +--------------------+--------+---------------------------------------------------------------------------------------+
      | protected_instance | String | Specifies the ID of the protected instance to which the replication pair is attached. |
      +--------------------+--------+---------------------------------------------------------------------------------------+

   .. _sdrs_05_0603__table5781813115015:

   .. table:: **Table 3** **record_metadata** field description

      +-----------------------+-----------------------+--------------------------------------------------------------------+
      | Parameter             | Type                  | Description                                                        |
      +=======================+=======================+====================================================================+
      | multiattach           | Boolean               | Specifies whether the disk in a replication pair is a shared disk. |
      +-----------------------+-----------------------+--------------------------------------------------------------------+
      | bootable              | Boolean               | Specifies whether the disk in a replication pair is a system disk. |
      +-----------------------+-----------------------+--------------------------------------------------------------------+
      | volume_size           | Integer               | Specifies the size of the disk in a replication pair. Unit: GB     |
      +-----------------------+-----------------------+--------------------------------------------------------------------+
      | volume_type           | String                | Specifies the type of the disk in a replication pair.              |
      |                       |                       |                                                                    |
      |                       |                       | The value can be as follows: **SAS**, or **SSD**.                  |
      |                       |                       |                                                                    |
      |                       |                       | -  **SSD**: the ultra-high I/O type                                |
      |                       |                       | -  **SAS**: the high I/O type                                      |
      +-----------------------+-----------------------+--------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
          "count": 1,
          "replications": [
              {
                  "id": "b93bc1c4-67ee-45a1-bc8a-d022fdd28811",
                  "name": "test_replication_name",
                  "description": "description_test",
                  "replication_model": "hypermetro",
                  "status": "available",
                  "progress": 0,
                  "replication_status": "active",
                  "attachment": [
                      {
                          "device": "/dev/vda",
                          "protected_instance": "8a7a6339-679b-452b-948c-144e0ef85d9e"
                      }
                  ],
                  "server_group_id": "c2aee29a-2959-4d01-9755-01cc76a4d17d",
                  "volume_ids": "48dda0c0-c800-46f2-9728-a519ff783d35,388b324a-a9d1-44a4-a00d-42085f22a9bc",
                  "priority_station": "source",
                  "fault_level": "0",
                  "created_at": "2018-05-04T03:43:24.108526",
                  "updated_at": "2018-05-04T03:44:28.322873",
                  "record_metadata": {
                      "multiattach": false,
                      "bootable": false,
                      "volume_size": 10,
                      "volume_type": "SATA"
                  }
              }
          ]
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
