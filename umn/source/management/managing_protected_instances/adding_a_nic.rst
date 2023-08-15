:original_name: sdrs_ug_pi_0006.html

.. _sdrs_ug_pi_0006:

Adding a NIC
============

Scenarios
---------

If more NICs are required for your protected instance, you can perform steps provided in this section to add a NIC to the protected instance.

**Prerequisites**
-----------------

-  The protection group is in the **Available** or **Protecting** state.
-  The protected instance is in the **Available** or **Protecting** state.
-  The subnet of the NIC to be added must belong to the same VPC of the protection group and protected instance.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. In the pane of the protection group, click **Protected Instances**.

   The operation page for the protection group is displayed.

#. On the **Protected Instances** tab, click the protected instance.

   The protected instance details page is displayed.

#. Click the **NICs** tab and click **Add NIC**.

#. Select the security group and subnet to be added.

   .. note::

      -  You can select multiple security groups. When multiple security groups are selected, the access rules of all the selected security groups apply on the server.
      -  If you want to add a NIC with a specified IP address, enter an IP address into the **Private IP Address** field.

#. Click **OK**.
