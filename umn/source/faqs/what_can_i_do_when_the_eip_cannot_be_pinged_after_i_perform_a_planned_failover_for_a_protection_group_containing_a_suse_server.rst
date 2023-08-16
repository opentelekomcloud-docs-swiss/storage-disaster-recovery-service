:original_name: sdrs_06_0402.html

.. _sdrs_06_0402:

What Can I Do When the EIP Cannot Be Pinged After I Perform a Planned Failover for a Protection Group Containing a SUSE Server?
===============================================================================================================================

Symptom
-------

The production site server in a protection group runs the SUSE OS. After users enable protection and perform a planned failover for the protection group, the EIP of the server cannot be pinged.

Root Cause
----------

After the planned failover, the server NIC name may already change. If the NIC has an EIP bound, the EIP cannot be pinged.

Handling Method
---------------

After the planned failover, delete the **/etc/udev/rules.d/70-persistent-net.rules** file on the DR site server and then restart it. The procedure is as follows.

#. Log in to the DR site server.

   a. Log in to the management console and click **Elastic Cloud Server** under **Computing**.

   b. In the server list, select the DR site server.

   c. Locate the row containing the server and click **Remote Login** in the **Operation** column.

      Log in to the server as prompted.

#. Run the following command to delete the file:

   **rm /etc/udev/rules.d/70-persistent-net.rules**

#. Run the following command to restart the DR site server:

   **reboot**
