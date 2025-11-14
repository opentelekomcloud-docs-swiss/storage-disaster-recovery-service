:original_name: sdrs_05_0403.html

.. _sdrs_05_0403:

Querying the Details of a Protection Group
==========================================

Function
--------

This API is used to query the details about a protection group, such as the protection group ID and name.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/server-groups/{server_group_id}

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

-  Request parameters

   None

-  Example request

   GET https://{Endpoint}/v1/{project_id}/server-groups/decf224d-87fe-403a-8721-037a1a45c287

Response
--------

-  Parameter description

   +-----------------------+-----------------------+--------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                        |
   +=======================+=======================+====================================================================+
   | server_group          | Object                | Specifies the details of a protection group.                       |
   |                       |                       |                                                                    |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0403__table137214610187>`. |
   +-----------------------+-----------------------+--------------------------------------------------------------------+

   .. _sdrs_05_0403__table137214610187:

   .. table:: **Table 1** **server_group** field description

      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                   | Type                  | Description                                                                                                                                              |
      +=============================+=======================+==========================================================================================================================================================+
      | id                          | String                | Specifies the ID of a protection group.                                                                                                                  |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | name                        | String                | Specifies the name of a protection group.                                                                                                                |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | description                 | String                | Specifies the description of a protection group.                                                                                                         |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | status                      | String                | Specifies the status of a protection group.                                                                                                              |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | For details, see :ref:`Protection Group Status <en-us_topic_0126152930>`.                                                                                |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | progress                    | Integer               | Specifies the synchronization progress of a protection group.                                                                                            |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | Unit: %                                                                                                                                                  |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | source_availability_zone    | String                | Specifies the production site AZ configured when a protection group is created.                                                                          |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | The value does not change after a planned failover or failover.                                                                                          |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | target_availability_zone    | String                | Specifies the DR site AZ configured when a protection group is created.                                                                                  |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | The value does not change after a planned failover or failover.                                                                                          |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | domain_id                   | String                | Specifies the ID of an active-active domain.                                                                                                             |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | domain_name                 | String                | Specifies the name of an active-active domain.                                                                                                           |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | priority_station            | String                | Specifies the current production site of a protection group.                                                                                             |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | -  **source**: indicates that the current production site AZ is the **source_availability_zone** value.                                                  |
      |                             |                       | -  **target**: indicates that the current production site AZ is the **target_availability_zone** value.                                                  |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | protected_instance_num      | Integer               | Specifies the number of protected instances in a protection group.                                                                                       |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_num             | Integer               | Specifies the number of replication pairs in a protection group.                                                                                         |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | disaster_recovery_drill_num | Integer               | Specifies the number of DR drills in a protection group.                                                                                                 |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | protected_status            | String                | Specifies whether protection is enabled or not.                                                                                                          |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | -  **started**: Protection is enabled.                                                                                                                   |
      |                             |                       | -  **stopped**: Protection is disabled.                                                                                                                  |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | .. note::                                                                                                                                                |
      |                             |                       |                                                                                                                                                          |
      |                             |                       |    The system is upgraded recently. For protection groups created after the upgrade, the value of this parameter is **null**.                            |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_status          | String                | Specifies the data synchronization status.                                                                                                               |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | -  **active**: Data has been synchronized.                                                                                                               |
      |                             |                       | -  **inactive**: Data is not synchronized.                                                                                                               |
      |                             |                       | -  **copying**: Data is being synchronized.                                                                                                              |
      |                             |                       | -  **active-stopped**: Data synchronization is stopped.                                                                                                  |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | .. note::                                                                                                                                                |
      |                             |                       |                                                                                                                                                          |
      |                             |                       |    The system is upgraded recently. For protection groups created after the upgrade, the value of this parameter is **null**.                            |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | health_status               | String                | Specifies the health status of a protection group.                                                                                                       |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | -  **normal**: The protection group is normal.                                                                                                           |
      |                             |                       | -  **abnormal**: The protection group is abnormal.                                                                                                       |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | .. note::                                                                                                                                                |
      |                             |                       |                                                                                                                                                          |
      |                             |                       |    The system is upgraded recently. For protection groups created after the upgrade, the value of this parameter is **null**.                            |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | source_vpc_id               | String                | Specifies the ID of the VPC for the production site.                                                                                                     |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | target_vpc_id               | String                | Specifies the ID of the VPC for the DR site.                                                                                                             |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | test_vpc_id                 | String                | Specifies the ID of the VPC used for a DR drill.                                                                                                         |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | .. note::                                                                                                                                                |
      |                             |                       |                                                                                                                                                          |
      |                             |                       |    This parameter is reserved.                                                                                                                           |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | dr_type                     | String                | Specifies the deployment model. The default value is **migration**, indicating migration within a VPC.                                                   |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | created_at                  | String                | Specifies the time when a protection group was created.                                                                                                  |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**.                                                   |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | updated_at                  | String                | Specifies the time when a protection group was updated.                                                                                                  |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | The default format is as follows: "yyyy-MM-dd HH:mm:ss.SSS", for example, **2019-04-01 12:00:00.000**.                                                   |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | protection_type             | String                | Specifies the protection mode.                                                                                                                           |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | -  **null**: indicates that data synchronization is performed at the replication consistency group level. No partial synchronization failure will occur. |
      |                             |                       | -  **replication-pair**: indicates that data synchronization is performed at the replication pair level.                                                 |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | replication_model           | String                | Specifies the protection mode.                                                                                                                           |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | .. note::                                                                                                                                                |
      |                             |                       |                                                                                                                                                          |
      |                             |                       |    This parameter is reserved.                                                                                                                           |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+
      | server_type                 | String                | Specifies the type of managed servers.                                                                                                                   |
      |                             |                       |                                                                                                                                                          |
      |                             |                       | -  **ECS**: indicates that ECSs are managed.                                                                                                             |
      +-----------------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------+

-  Example response

   .. code-block::

      {
          "server_group": {
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
              "server_type": "ECS",
              "created_at": "2019-05-22 08:16:54.413",
              "updated_at": "2019-05-23 09:11:10.856",
              "protection_type": "replication-pair",
              "replication_model": null
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

   In the preceding example, **error** indicates a general error, for example, **badrequest** or **itemNotFound**. An example is provided as follows:

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
