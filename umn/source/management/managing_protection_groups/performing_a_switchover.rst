:original_name: sdrs_ug_pg_0002.html

.. _sdrs_ug_pg_0002:

Performing a Switchover
=======================

Scenarios
---------

After you perform a switchover, services at the production site are switched to the DR site, and services at the DR site are switched over to the production site. :ref:`Table 1 <sdrs_ug_pg_0002__table938371263712>` shows the direction change.

.. _sdrs_ug_pg_0002__table938371263712:

.. table:: **Table 1** DR direction change after a switchover

   ====== =============== =======
   ``-``  Production Site DR Site
   ====== =============== =======
   Before AZ1             AZ2
   After  AZ2             AZ1
   ====== =============== =======

After the switchover, data synchronization continues, but the DR direction is changed from the DR site to the production site. You can perform a switchover when you are certain that the production site will encounter an interruption. For example, if the production site (AZ1) is going to encounter a power failure, you can perform a switchover to switch services in AZ1 to the DR site (AZ2). The switchover does not affect data synchronization of the protection group.

SDRS will migrate NICs on the server during the switchover. Once completed, the IP, EIP, and MAC addresses of the production site server will be migrated to the DR site server, so that the IP, EIP, and MAC addresses remain the same.

.. note::

   -  Check the status to ensure that all the servers in the protection group are stopped before a switchover.
   -  During a switchover, do not start the servers in the protection group. Or, the switchover may fail.
   -  Once a switchover is complete, data synchronization will not stop, only the synchronization direction will reverse.
   -  Once a switchover is complete, the status of the protection group changes to **Protecting**. Then, you need to go to the protected instance details page and start the production site server.


.. figure:: /_static/images/en-us_image_0288665337.png
   :alt: **Figure 1** Performing a switchover

   **Figure 1** Performing a switchover

Notes
-----

For Linux servers with Cloud-Init installed, if you have changed **hostname** of the production site server before you perform a switchover for the first time, this modification will not synchronize to the DR site server.

To resolve this problem, see :ref:`What Can I Do If hostname of the Production Site Server and DR Site Server Are Different After a Switchover or Failover? <sdrs_06_0404>`

Prerequisites
-------------

-  All the servers in the protection group are stopped.
-  The protection group has replication pairs.
-  Protection is enabled for the protection group, and the protection group is in the **Protecting** or **Switchover failed** state.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and choose **Storage** > **Storage Disaster Recovery Service**.

   The **Storage Disaster Recovery Service** page is displayed.

#. In the pane of the desired protection group, click **Protected Instances**.

#. In the upper right corner of the page, click **Execute Switchover**.

#. In the displayed dialog box, check whether all the servers in this protection group are stopped.

   -  If yes, go to step :ref:`6 <sdrs_ug_pg_0002__li812255515532>`.
   -  If no, select the servers to be stopped and click **Stop**.

#. .. _sdrs_ug_pg_0002__li812255515532:

   In the displayed dialog box, click **Execute Switchover**.

   .. note::

      During a switchover, do not start the servers in the protection group. Or, the switchover may fail.
