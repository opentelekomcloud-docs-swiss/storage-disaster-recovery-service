:original_name: sdrs_ug_pg_0001.html

.. _sdrs_ug_pg_0001:

Disabling Protection
====================

Scenarios
---------

If you want to disable protection for all resources in a specified protection group, you can perform steps provided in this section.

Once the protection is disabled, data synchronization for all protected instances in the protection group will stop.

**Prerequisites**
-----------------

-  The protection group has replication pairs.

-  The protection group is in the **Protecting** or **Disabling protection failed** state.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. In the pane of the desired protection group, click **Protected Instances**.

   The operation page for the protection group is displayed.

#. In the upper right corner of the page, click **Disable Protection**.

#. In the displayed dialog box, click **Yes**.

   Once the protection is disabled, data synchronization between the production site and DR site for all protected instances in the protection group will stop.
