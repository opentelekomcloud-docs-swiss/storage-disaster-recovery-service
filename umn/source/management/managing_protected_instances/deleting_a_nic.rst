:original_name: sdrs_ug_pi_0007.html

.. _sdrs_ug_pi_0007:

Deleting a NIC
==============

Scenarios
---------

A protected instance can have up to 12 NICs, including one primary NIC that cannot be deleted. You can perform steps provided in this section to delete a NIC other than the primary one.

**Prerequisites**
-----------------

-  The protection group is in the **Available** or **Protecting** state.
-  The protected instance is in the **Available** or **Protecting** state.
-  The primary NIC cannot be deleted.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. In the pane of the protection group for which a NIC is to be deleted from the protected instance, click **Protected Instances**.

   The operation page for the protection group is displayed.

#. On the **Protected Instances** tab, click the protected instance.

   The protected instance details page is displayed.

#. Click the **NICs** tab. Then, click **Delete** in the row that contains the NIC to be deleted.

#. Click **Yes**.
