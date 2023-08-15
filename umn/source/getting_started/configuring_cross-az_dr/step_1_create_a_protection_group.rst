:original_name: en-us_topic_0108180805.html

.. _en-us_topic_0108180805:

Step 1: Create a Protection Group
=================================

Scenarios
---------

You can specify two AZs as the source and target AZs, and create a protection group. Then, you can create protected instances and replication pairs in this protection group.

Verify the servers at the production and DR sites before you create a protection group. In this version, only the VPC migration deployment model is supported. Specifically, the servers at the production and DR sites must be in different AZs but in the same VPC.


.. figure:: /_static/images/en-us_image_0288665357.png
   :alt: **Figure 1** Creating a protection group

   **Figure 1** Creating a protection group

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. Click **Create Protection Group**.

   The **Create Protection Group** page is displayed.


   .. figure:: /_static/images/en-us_image_0000001193113788.png
      :alt: **Figure 2** Creating a protection group

      **Figure 2** Creating a protection group

#. Configure the basic information about the protection group listed in :ref:`Table 1 <en-us_topic_0108180805__table0120161710336>`.

   .. note::

      All the parameters in the following table are mandatory.

   .. _en-us_topic_0108180805__table0120161710336:

   .. table:: **Table 1** Parameter description

      +-----------------------+----------------------------------------------------------------------------------------------------------------------------+------------------------+
      | Parameter             | Description                                                                                                                | Example Value          |
      +=======================+============================================================================================================================+========================+
      | Region                | A region is a geographic area where resources used by servers are located.                                                 | az-01                  |
      |                       |                                                                                                                            |                        |
      |                       | If the region is incorrect, click the drop-down list for correction.                                                       |                        |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------+------------------------+
      | DR Direction          | -  Production site: Select the AZ of the production site server.                                                           | Production site: az-01 |
      |                       | -  DR site: Select the AZ of the DR site server.                                                                           |                        |
      |                       |                                                                                                                            | DR site: az-02         |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------+------------------------+
      | Deployment Model      | Currently, only the VPC migration model is supported. All resources at the production and DR sites belong to the same VPC. | VPC migration          |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------+------------------------+
      | VPC                   | Specifies the VPC where the protection group is located.                                                                   | vpc-test               |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------+------------------------+
      | Protection Group Name | Enter the protection group name. It is used for group classification and search.                                           | protection_group_001   |
      +-----------------------+----------------------------------------------------------------------------------------------------------------------------+------------------------+

#. Click **Create Now**.

#. Click **Back to Protection Group List** to return to the SDRS homepage and query the protection group status.

   If the protection group is displayed in the **Storage Disaster Recovery Service** page and its status is **Available** (|image1|), the protection group has been created successfully.

.. |image1| image:: /_static/images/en-us_image_0288665395.png
