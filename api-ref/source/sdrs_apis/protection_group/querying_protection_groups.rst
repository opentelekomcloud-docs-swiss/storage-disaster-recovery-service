:original_name: sdrs_05_0402.html

.. _sdrs_05_0402:

Querying Protection Groups
==========================

Function
--------

This API is used to query all protection groups of the current tenant.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/server-groups

-  Parameter description

   ========== ========= ====== =========================
   Parameter  Mandatory Type   Description
   ========== ========= ====== =========================
   project_id Yes       String Specifies the project ID.
   ========== ========= ====== =========================

-  **Request filter** field description

   +-------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                                                                                                                   |
   +===================+=================+=================+===============================================================================================================================================================================+
   | limit             | No              | Integer         | Specifies the maximum number of results returned each time. The value is a positive integer from 0 to 1000. The default value is **1000**.                                    |
   +-------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | offset            | No              | Integer         | Specifies the offset of each request. The default value is **0**. The value must be a number and cannot be negative.                                                          |
   +-------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | status            | No              | String          | Specifies the protection group status.                                                                                                                                        |
   |                   |                 |                 |                                                                                                                                                                               |
   |                   |                 |                 | For details, see :ref:`Protection Group Status <en-us_topic_0126152930>`.                                                                                                     |
   +-------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | name              | No              | String          | Specifies the name of a protection group.                                                                                                                                     |
   |                   |                 |                 |                                                                                                                                                                               |
   |                   |                 |                 | Fuzzy search is supported.                                                                                                                                                    |
   +-------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | query_type        | No              | String          | Specifies the query type.                                                                                                                                                     |
   |                   |                 |                 |                                                                                                                                                                               |
   |                   |                 |                 | -  **status_abnormal**: indicates to query protection groups in the abnormal status.                                                                                          |
   |                   |                 |                 | -  **stop_protected**: indicates to query protection groups for which the protection is disabled.                                                                             |
   |                   |                 |                 | -  **period_no_dr_drill**: indicates to query the protection groups for which the no DR drills have been performed in a specified duration. The default duration is 3 months. |
   |                   |                 |                 | -  This parameter is invalid when the value is set to **general** or left empty.                                                                                              |
   +-------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | availability_zone | No              | String          | Specifies the current production site AZ of a protection group.                                                                                                               |
   |                   |                 |                 |                                                                                                                                                                               |
   |                   |                 |                 | You can obtain this value by calling the API described in :ref:`Querying an Active-Active Domain <sdrs_05_0301>`.                                                             |
   +-------------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{Endpoint}/v1/{project_id}/server-groups

Response
--------

-  Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                 |
   +=======================+=======================+=============================================================================+
   | server_groups         | Array of objects      | Specifies the information about protection groups.                          |
   |                       |                       |                                                                             |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0402__table503353570>`.             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------+
   | count                 | Integer               | Specifies the number of protection groups that meet the filtering criteria. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------+

   .. _sdrs_05_0402__table503353570:

   .. table:: **Table 1** **server_groups** field description

      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                   | Type                  | Description                                                                                                                                                         |
      +=============================+=======================+=====================================================================================================================================================================+
      | id                          | String                | Specifies the ID of a protection group.                                                                                                                             |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name                        | String                | Specifies the name of a protection group.                                                                                                                           |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | description                 | String                | Specifies the description of a protection group.                                                                                                                    |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | status                      | String                | Specifies the status of a protection group. For details, see :ref:`Protection Group Status <en-us_topic_0126152930>`.                                               |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | progress                    | Integer               | Specifies the synchronization progress of a protection group.                                                                                                       |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | Unit: %                                                                                                                                                             |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | source_availability_zone    | String                | Specifies the production site AZ configured when a protection group is created.                                                                                     |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | The value does not change after a planned failover or failover.                                                                                                     |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | target_availability_zone    | String                | Specifies the DR site AZ configured when a protection group is created.                                                                                             |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | The value does not change after a planned failover or failover.                                                                                                     |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | domain_id                   | String                | Specifies the ID of an active-active domain.                                                                                                                        |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | domain_name                 | String                | Specifies the name of an active-active domain.                                                                                                                      |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | priority_station            | String                | Specifies the current production site of a protection group.                                                                                                        |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | -  **source**: indicates that the current production site AZ is the **source_availability_zone** value.                                                             |
      |                             |                       | -  **target**: indicates that the current production site AZ is the **target_availability_zone** value.                                                             |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | protected_instance_num      | Integer               | Specifies the number of protected instances in a protection group.                                                                                                  |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_num             | Integer               | Specifies the number of replication pairs in a protection group.                                                                                                    |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | disaster_recovery_drill_num | Integer               | Specifies the number of DR drills in a protection group.                                                                                                            |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | protected_status            | String                | Specifies whether protection is enabled or not.                                                                                                                     |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | -  **started**: Protection is enabled.                                                                                                                              |
      |                             |                       | -  **stopped**: Protection is disabled.                                                                                                                             |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | .. note::                                                                                                                                                           |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       |    The system has been upgraded. For newly protection groups, the value of this parameter is **null**.                                                              |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_status          | String                | Specifies the data synchronization status.                                                                                                                          |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | -  **active**: Data has been synchronized.                                                                                                                          |
      |                             |                       | -  **inactive**: Data is not synchronized.                                                                                                                          |
      |                             |                       | -  **copying**: Data is being synchronized.                                                                                                                         |
      |                             |                       | -  **active-stopped**: Data synchronization is stopped.                                                                                                             |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | .. note::                                                                                                                                                           |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       |    The system has been upgraded. For newly protection groups, the value of this parameter is **null**.                                                              |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | health_status               | String                | Specifies the health status of a protection group.                                                                                                                  |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | -  **normal**: The protection group is normal.                                                                                                                      |
      |                             |                       | -  **abnormal**: The protection group is abnormal.                                                                                                                  |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | .. note::                                                                                                                                                           |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       |    The system is upgraded recently. For protection groups created after the upgrade, the value of this parameter is **null**.                                       |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | source_vpc_id               | String                | Specifies the ID of the VPC for the production site.                                                                                                                |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | target_vpc_id               | String                | Specifies the ID of the VPC for the DR site.                                                                                                                        |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | test_vpc_id                 | String                | Specifies the ID of the VPC used for a DR drill. This parameter is not used in the current version.                                                                 |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | dr_type                     | String                | Specifies the deployment model. The default value is **migration**, indicating migration within a VPC.                                                              |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | created_at                  | String                | Specifies the time when a protection group was created.                                                                                                             |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**.                                                              |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | updated_at                  | String                | Specifies the time when a protection group was updated.                                                                                                             |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**.                                                              |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | protection_type             | String                | Specifies the protection mode.                                                                                                                                      |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | -  **replication-pair**: indicates that data synchronization is performed at the replication pair level.                                                            |
      |                             |                       | -  **null**: indicates that data synchronization is performed at the replication consistency group level.                                                           |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | .. note::                                                                                                                                                           |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       |    The system has been upgraded. Data synchronization is performed at the replication pair level for all resources, and the returned value is **replication-pair**. |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_model           | String                | Specifies the protection mode.                                                                                                                                      |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | .. note::                                                                                                                                                           |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       |    This parameter is reserved.                                                                                                                                      |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | server_type                 | String                | Specifies the type of managed servers.                                                                                                                              |
      |                             |                       |                                                                                                                                                                     |
      |                             |                       | -  **ECS**: indicates that ECSs are managed.                                                                                                                        |
      +-----------------------------+-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
         "count": 2,
         "server_groups": [
              {
                  "id": "40df180b-9fe2-471a-8c64-1b758dc84189",
                  "name": "testname",
                  "description": "description",
                  "source_availability_zone": "AZ01",
                  "target_availability_zone": "AZ02",
                  "domain_id": "fb4bb8e3-a574-4437-a156-78c916aeea4d",
                  "domain_name": "ActiveactiveDomain",
                  "status": "available",
                  "protected_status": null,
                  "replication_status": null,
                  "health_status": null,
                  "progress": 0,
                  "priority_station": "source",
                  "protected_instance_num": 0,
                  "replication_num": 0,
                  "disaster_recovery_drill_num": 0,
                  "source_vpc_id": "046852ef-c49d-409b-8389-546aaaa5701f",
                  "target_vpc_id": "046852ef-c49d-409b-8389-546aaaa5701f",
                  "test_vpc_id": null,
                  "dr_type": "migration",
                  "server_type":"ECS"
                  "created_at": "2019-05-23 03:51:58.256",
                  "updated_at": "2019-05-23 07:48:12.484",
                  "protection_type": "replication-pair",
                  "replication_model": null
              },
              {
                  "id": "decf224d-87fe-403a-8721-037a1a45c287",
                  "name": "Protection-Group-lwx",
                  "description": null,
                  "source_availability_zone": "AZ01",
                  "target_availability_zone": "AZ02",
                  "domain_id": "fb4bb8e3-a574-4437-a156-78c916aeea4d",
                  "domain_name": "ActiveactiveDomain",
                  "status": "available",
                  "protected_status": null,
                  "replication_status": null,
                  "health_status": null,
                  "progress": 0,
                  "priority_station": "source",
                  "protected_instance_num": 0,
                  "replication_num": 0,
                  "disaster_recovery_drill_num": 0,
                  "source_vpc_id": "046852ef-c49d-409b-8389-546aaaa5701f",
                  "target_vpc_id": "046852ef-c49d-409b-8389-546aaaa5701f",
                  "test_vpc_id": null,
                  "dr_type": "migration",
                  "server_type":ECS,
                  "created_at": "2019-05-22 08:16:54.413",
                  "updated_at": "2019-05-23 07:48:12.493",
                  "protection_type": "replication-pair",
                  "replication_model": null
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
