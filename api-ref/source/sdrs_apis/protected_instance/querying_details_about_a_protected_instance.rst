:original_name: sdrs_05_0504.html

.. _sdrs_05_0504:

Querying Details About a Protected Instance
===========================================

Function
--------

This API is used to query the details about a protected instance, such as the protected instance ID and name.

Constraints and Limitations
---------------------------

None

URI
---

-  URI format

   GET /v1/{project_id}/protected-instances/{protected_instance_id}

-  Parameter description

   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory       | Type            | Description                                                                                                   |
   +=======================+=================+=================+===============================================================================================================+
   | project_id            | Yes             | String          | Specifies the project ID.                                                                                     |
   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | protected_instance_id | Yes             | String          | Specifies the ID of a protected instance.                                                                     |
   |                       |                 |                 |                                                                                                               |
   |                       |                 |                 | You can obtain this value by calling the API described in :ref:`Querying Protected Instances <sdrs_05_0503>`. |
   +-----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+

Request
-------

-  Request parameters

   None

-  Example request

   GET https://{Endpoint}/v1/{project_id}/protected-instances/50f5091e-9e9e-473c-a932-2a2cbcbeb1ff

Response
--------

-  Parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                     |
   +=======================+=======================+=================================================================+
   | protected_instance    | Object                | Specifies the details about a protected instance.               |
   |                       |                       |                                                                 |
   |                       |                       | For details, see :ref:`Table 1 <sdrs_05_0504__table503353570>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------+

   .. _sdrs_05_0504__table503353570:

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

   .. table:: **Table 2** **attachment** field description

      =========== ====== =======================================
      Parameter   Type   Description
      =========== ====== =======================================
      replication String Specifies the ID of a replication pair.
      device      String Specifies the device name.
      =========== ====== =======================================

   .. table:: **Table 3** **tags** field description

      ========= ====== ========================
      Parameter Type   Description
      ========= ====== ========================
      key       String Specifies the tag key.
      value     String Specifies the tag value.
      ========= ====== ========================

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
          "protected_instance": {
              "id": "50f5091e-9e9e-473c-a932-2a2cbcbeb1ff",
              "name": "ecs_sdrs_test",
              "description": "1111",
              "server_group_id": "943c7d15-0371-4b89-b1a6-db1ef35c9263",
              "status": "available",
              "progress": 0,
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
                      "value": "dddd"
                    }
                  ],
               "metadata": {}
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
