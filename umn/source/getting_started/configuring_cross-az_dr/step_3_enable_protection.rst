:original_name: en-us_topic_0110046974.html

.. _en-us_topic_0110046974:

Step 3: Enable Protection
=========================

Scenarios
---------

If you want to enable protection for all resources in a specified protection group, you can perform steps provided in this section.

When data is written to the disks of the production site server, SDRS synchronizes the data to the disks of the DR site server in real time. Both the production site and DR site can use Cloud Server Backup Service (CSBS) and Volume Backup Service (VBS) to back up the servers and disks.


.. figure:: /_static/images/en-us_image_0288665401.png
   :alt: **Figure 1** Enabling protection

   **Figure 1** Enabling protection

**Prerequisites**
-----------------

-  The protection group has replication pairs.
-  The protection group is in the **Available** or **Enabling protection failed** state.
-  After you create a protected instance and enable protection on servers at the production site, modifications to the **Hostname**, **Name**, **Security Group**, **Agency**, **ECS Group**, **Tags**, and **Auto Recovery** configurations of servers on the production site will not synchronize to the servers at the DR site. You can manually add the configuration items to the servers at the DR site on the management console.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. In the pane of the desired protection group, click **Enable Protection**.


   .. figure:: /_static/images/en-us_image_0288665358.png
      :alt: **Figure 2** Enabling protection

      **Figure 2** Enabling protection

#. In the displayed dialog box, click **Yes**.

   Once protection is enabled, data synchronization starts.

   .. note::

      The synchronization time is in direct proportion to the disk capacity. Larger disk capacity requires longer synchronization time.
