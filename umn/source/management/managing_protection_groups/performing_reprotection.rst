:original_name: sdrs_ug_pg_0006.html

.. _sdrs_ug_pg_0006:

Performing Reprotection
=======================

Scenarios
---------

Once the failover is started, data synchronization stops. After the failover is complete, the protection group is in the **Protection disabled** state. To restart data synchronization, perform steps provided in this section.

**Prerequisites**
-----------------

-  The protection group has replication pairs.
-  The protection group is in the **Failover complete** or **Re-enabling protection failed**.
-  The DR site server is stopped.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. In the pane of the desired protection group, click **Protected Instances**.

#. In the upper right corner of the page, click **More** and choose **Reprotect** from the drop-down list.

   The **Reprotect** dialog box is displayed.

#. Check whether all the DR site servers in this protection group are stopped.

   -  If yes, go to step :ref:`6 <sdrs_ug_pg_0006__li812255515532>`.
   -  If no, select the servers to be stopped and click **Stop**.

#. .. _sdrs_ug_pg_0006__li812255515532:

   On the **Reprotect** dialog box, click **Reprotect**.

   During the reprotection, do not start the DR site servers in the protection group. Otherwise, the reprotection may fail.
