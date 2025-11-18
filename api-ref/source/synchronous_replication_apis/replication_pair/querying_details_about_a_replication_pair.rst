:original_name: sdrs_05_0604.html

.. _sdrs_05_0604:

Querying Details About a Replication Pair
=========================================

Function
--------

This API is used to query the details about a replication pair.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/replications/{replication_id}

-  Parameter description

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory             | Description                                                                                                 |
   +=======================+=======================+=============================================================================================================+
   | project_id            | Yes                   | Specifies the project ID.                                                                                   |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------+
   | replication_id        | Yes                   | Specifies the ID of a replication pair.                                                                     |
   |                       |                       |                                                                                                             |
   |                       |                       | You can obtain this value by calling the API described in :ref:`Querying Replication Pairs <sdrs_05_0603>`. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{Endpoint}/v1/{project_id}/replications/b93bc1c4-67ee-45a1-bc8a-d022fdd28811

Response
--------

-  Parameter description

   +-----------------------+-----------------------+-------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                       |
   +=======================+=======================+===================================================================+
   | replication           | Object                | Specifies the information about a replication pair.               |
   |                       |                       |                                                                   |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0604__table84048224492>`. |
   +-----------------------+-----------------------+-------------------------------------------------------------------+

   .. _sdrs_05_0604__table84048224492:

   .. table:: **Table 1** **replication** field description

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
      | status                | String                | Specifies the status of a replication pair. For details, see :ref:`Replication Pair Status <en-us_topic_0126152932>`.                        |
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
      |                       |                       | For details, see :ref:`Table 2 <sdrs_05_0604__table03591028145217>`.                                                                         |
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
      |                       |                       | For details, see :ref:`Table 3 <sdrs_05_0604__table1636242815523>`.                                                                          |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+
      | failure_detail        | String                | Specifies the error code returned only when **status** of a replication pair is **error**.                                                   |
      |                       |                       |                                                                                                                                              |
      |                       |                       | For details, see the returned value in :ref:`Error Codes <en-us_topic_0113127626>`.                                                          |
      +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------+

   .. _sdrs_05_0604__table03591028145217:

   .. table:: **Table 2** **attachment** field description

      +--------------------+--------+---------------------------------------------------------------------------------------+
      | Parameter          | Type   | Description                                                                           |
      +====================+========+=======================================================================================+
      | device             | String | Specifies the device name.                                                            |
      +--------------------+--------+---------------------------------------------------------------------------------------+
      | protected_instance | String | Specifies the ID of the protected instance to which the replication pair is attached. |
      +--------------------+--------+---------------------------------------------------------------------------------------+

   .. _sdrs_05_0604__table1636242815523:

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
          "replication":
              {
                  "id": "b93bc1c4-67ee-45a1-bc8a-d022fdd28811",
                  "name": "test_sdrs_replication",
                  "description": "test_description",
                  "replication_model": "hypermetro",
                  "status": "available",
                  "progress": 0,
                  "replication_status": "active",
                  "attachment": [
                      {
                          "device": "/dev/vda",
                          "protected_instance": "8a7a6339-679b-452b-948c-144e0ef85d9c"
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
