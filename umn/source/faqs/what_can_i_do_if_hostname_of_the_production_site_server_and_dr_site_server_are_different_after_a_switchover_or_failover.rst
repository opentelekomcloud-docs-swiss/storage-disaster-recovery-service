:original_name: sdrs_06_0404.html

.. _sdrs_06_0404:

What Can I Do If hostname of the Production Site Server and DR Site Server Are Different After a Switchover or Failover?
========================================================================================================================

Symptom
-------

Users have changed **hostname** of the production site server before they perform a switchover or failover for the first time. After the switchover or failover, users start the DR site server and find that **hostname** of the DR site server is not updated accordingly.

Possible Causes
---------------

For Linux servers, if you have changed **hostname** of the production site server before you perform a switchover or failover for the first time, this modification will not synchronize to the DR site server.

Prerequisites
-------------

-  The production site server is a Linux server with Cloud-Init installed.
-  **hostname** of the production site server has been changed.

Solution 1 (If You Have Not Performed a Switchover or Failover)
---------------------------------------------------------------

Set **preserve_hostname: false** to **preserve_hostname: true** in the Cloud-Init configuration file **/etc/cloud/cloud.cfg** to ensure that **hostname** of the production site server and DR site server are the same after you enable protection.

The procedure is as follows:

#. Log in to the production site server.

#. Run the following command to edit the **/etc/cloud/cloud.cfg** configuration file:

   **sudo vim /etc/cloud/cloud.cfg**

#. Modify **preserve_hostname**.

   -  If **preserve_hostname: false** is already available in the **/etc/cloud/cloud.cfg** configuration file, change it to **preserve_hostname: true**.
   -  If **preserve_hostname: false** is unavailable in the **/etc/cloud/cloud.cfg** configuration file, add **preserve_hostname: true** before **cloud_init_modules**.

#. Perform a switchover or failover.

   After the switchover or failover, **hostname** of the DR site server and production site server are the same.

Solution 2 (If You Have Performed a Switchover or Failover)
-----------------------------------------------------------

If you have not modified configuration file **/etc/cloud/cloud.cfg** before the switchover or failover, log in to the DR site server and manually change **hostname** of the DR site server to that of the production site server.
