:original_name: sdrs_ug_rp_0002.html

.. _sdrs_ug_rp_0002:

Expanding Capacity of a Replication Pair
========================================

Scenarios
---------

If the replication pair capacity of your protection group cannot meet your service requirements, you can expand the capacities of replication pairs. Replication pair capacity cannot be reduced, and their capacity expansion cannot be rolled back.

After you expand the capacity of a replication pair, capacities of both the production and DR site disks are changed.

Prerequisites
-------------

-  The replication pair must be in the **Available**, **Protecting**, or **Expansion failed** state.
-  Disks in the replication pair are in the **Available** or **In-use** state.
-  Capacity expansion is not supported for replication pairs consist of yearly/monthly disks. To expand the capacity of such a replication pair, delete the replication pair, expand the capacity of the production site disk, and then use the disk to create a new replication pair.

.. note::

   -  For replication pairs consist of non-shared disks:

      If the disk status is **In-use**, the replication pair capacity can be expanded only when online capacity expansion is supported. If online capacity expansion is not supported, the **Expand Capacity** button will be grayed out.

   -  For replication pairs consist of shared disks:

      Online capacity expansion is not supported.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. Locate the protection group where you want to expand the replication pair capacity and click **Replication Pairs**.

   The protection group details page is displayed.

#. On the **Replication Pairs** tab, locate the row containing the target replication pair and click **Expand Capacity** in the **Operation** column.

   The **Expand Capacity** page is displayed.

#. On the **Expand Capacity** page, confirm the replication pair information, configure **Add Capacity**, and click **Next**.

#. Confirm the information and click **Submit**.

   If you want to modify the configuration, click **Previous**.

--------------

Copyright © Huawei Technologies Co., Ltd.
