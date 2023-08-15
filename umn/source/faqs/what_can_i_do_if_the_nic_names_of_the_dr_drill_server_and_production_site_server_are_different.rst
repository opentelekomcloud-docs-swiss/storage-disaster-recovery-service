:original_name: sdrs_06_0403.html

.. _sdrs_06_0403:

What Can I Do If the NIC Names of the DR Drill Server and Production Site Server Are Different?
===============================================================================================

Symptom
-------

The production site server runs the SUSE OS. After users create a DR drill using this server, the NIC names of the DR drill server are different from those of the production site server.

The following is an example:

A production site server running Novell SUSE Linux Enterprise Server 12 SP3 64-bit has five NICs attached. Log in to the production site server and query the NIC names (eth0 to eth4).


.. figure:: /_static/images/en-us_image_0288665316.png
   :alt: **Figure 1** Production site server NIC names

   **Figure 1** Production site server NIC names

Log in to the DR drill server and query the NIC names (eth5 to eth9).


.. figure:: /_static/images/en-us_image_0288665320.png
   :alt: **Figure 2** DR drill server NIC names

   **Figure 2** DR drill server NIC names

The NIC names of the DR drill server are different from those of the production site server.

Root Cause
----------

The NIC names may change when users create a DR drill.

Handling Method
---------------

After the DR drill, delete the **/etc/udev/rules.d/70-persistent-net.rules** file on the DR drill server and then restart it. The procedure is as follows.

#. Log in to the DR drill server.

   a. Log in to the management console and click **Elastic Cloud Server** under **Computing**.

   b. In the server list, select the DR drill server.

   c. Locate the row containing the server and click **Remote Login** in the **Operation** column.

      Log in to the server as prompted.

#. Run the following command to delete the file:

   **rm /etc/udev/rules.d/70-persistent-net.rules**

#. Run the following command to restart the DR drill server:

   **reboot**
