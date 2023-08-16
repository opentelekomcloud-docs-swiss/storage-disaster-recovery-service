:original_name: sdrs_ug_rp_0001.html

.. _sdrs_ug_rp_0001:

Creating a Replication Pair
===========================

Scenarios
---------

You can create replication pairs for desired disks and add the replication pairs to a specified protection group. When you create a replication pair:

-  If the protection group is in the **Available** state, protection is disabled. The production site disk and DR site disk have formed a replication pair, but data synchronization is not started. To start data synchronization, enable protection.
-  If the protection group is in the **Protecting** state, protection is enabled. After you create a replication pair, data synchronization is automatically started.

.. note::

   After a replication pair is created, the default name of the DR site disk is the same as the name of the production site disk, but their IDs are different.

   To modify a disk name, click the disk name on the replication pair details page to switch to the disk details page and modify it.

**Prerequisites**
-----------------

-  The protection group is in the **Available** or **Protecting** state.
-  If **Server Type** of the protection group is **ECS**, the disks used to create the replication pair are in the **Available** state.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. In the pane of the protection group for which replication pairs are to be added, click **Replication Pairs**.

   The operation page for the protection group is displayed.

#. On the **Replication Pairs** tab, click **Create Replication Pair**.

   The **Create Replication Pair** page is displayed.


   .. figure:: /_static/images/en-us_image_0000001237919697.png
      :alt: **Figure 1** Creating a replication pair

      **Figure 1** Creating a replication pair

#. Configure the basic information about the replication pair listed in :ref:`Table 1 <sdrs_ug_rp_0001__en-us_topic_0110037559_table14113172215131>`.

   .. _sdrs_ug_rp_0001__en-us_topic_0110037559_table14113172215131:

   .. table:: **Table 1** Parameter description

      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
      | Parameter             | Description                                                                                                                                       | Example Value                        |
      +=======================+===================================================================================================================================================+======================================+
      | Protection Group Name | Indicates the name of the protection group to which the replication pair to be created belongs. You do not need to configure it.                  | Protection-Group-test                |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
      | Protection Group ID   | Specifies the ID of a protection group.                                                                                                           | 619c57e9-3927-48f8-ad14-3e293260b8a0 |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
      | DR Direction          | Indicates the replication direction of the protection group to which the replication pair to be created belongs. You do not need to configure it. | ``-``                                |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
      | Production Site       | Specifies the AZ of the production site.                                                                                                          | ``-``                                |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
      | Production Site Disk  | This parameter is mandatory.                                                                                                                      | EVS                                  |
      |                       |                                                                                                                                                   |                                      |
      |                       | Select a disk.                                                                                                                                    |                                      |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+
      | Replication Pair Name | Indicates the replication pair name. This parameter is mandatory.                                                                                 | replication_001                      |
      |                       |                                                                                                                                                   |                                      |
      |                       | Configure this parameter when you create a replication pair. Then, you can use this name to classify and search this replication pair.            |                                      |
      +-----------------------+---------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------+

#. Click **Create Now**.

#. On the **Confirm** page, you can confirm the replication pair information.

   -  If you do not need to modify the information, click **Submit**.
   -  If you need to modify the information, click **Previous**.

#. Click **Back to Protection Group Details Page** and query the replication pairs of the protection group.

   If the replication pair status changes to **Available** or **Protecting**, the replication pair has been created successfully.
