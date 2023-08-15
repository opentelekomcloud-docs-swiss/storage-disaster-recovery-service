:original_name: sdrs_04_0000.html

.. _sdrs_04_0000:

Getting Started
===============

This section describes how to create a protection group by calling APIs.

.. note::

   The validity period of a token obtained from IAM is 24 hours. If you want to use a token for authentication, cache it to avoid frequently calling the IAM API.

Involved APIs
-------------

If you use a token for authentication, you must obtain the token and add **X-Auth-Token** to the request header of the service API when making an API call.

-  IAM API used to obtain the token
-  SDRS API used to create a protection group

Procedure
---------

#. Obtain the token by performing steps provided in :ref:`Authentication <sdrs_03_0003>`.

#. Send **POST https://**\ *SDRS endpoint*\ **/v1/{project_id}/server-groups**.

#. Add **X-Auth-Token** to the request header.

#. Specify the following parameters in the request body:

   .. code-block::

      {
          "server_group": {
              "name":"testname",    //Protection group name
              "description":"description",      //Protection group description
              "source_availability_zone": "az1.ac1",    //Production site AZ name of the protection group
              "target_availability_zone": "az2.ac2",    //DR site AZ name of the protection group
              "domain_id":"bccc426c-7dc4-4196-b4d8-372051f306fa",     //Active-active domain ID
              "source_vpc_id":"a9497554-3137-4a04-92bf-4be0ccdc8afe",   //Production site VPC ID
              "dr_type":"migration"     //Deployment model of the protection group
          }
      }

   If the request is successful, a job ID is returned.

   If the request fails, an error code and error information are returned. For details, see :ref:`Error Codes <en-us_topic_0113127626>`.

5. Query job details using the job ID by referring to :ref:`Querying the Job Status <sdrs_05_0101>`.

   If the returned job status is **SUCCESS**, the protection group is successfully created.

6. Obtain the protection group ID from the body of the job. You can query, delete, or update the protection group using this ID.
