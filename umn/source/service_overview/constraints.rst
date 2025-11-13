:original_name: en-us_topic_0110981899.html

.. _en-us_topic_0110981899:

Constraints
===========

Before using SDRS, learn about the constraints listed in :ref:`Table 1 <en-us_topic_0110981899__table14007370>`.

.. _en-us_topic_0110981899__table14007370:

.. table:: **Table 1** Constraints

   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Constraint                        | Description                                                                                                                                                                                            |
   +===================================+========================================================================================================================================================================================================+
   | Computing                         | Constraints on server types:                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                        |
   |                                   | -  GPU-accelerated, FPGA-accelerated, and C6 ECSs are not supported.                                                                                                                                   |
   |                                   |                                                                                                                                                                                                        |
   |                                   |    -  Kunpeng ECSs are not supported.                                                                                                                                                                  |
   |                                   |    -  x86 ECSs with GPU-accelerated and FPGA-accelerated types are not supported.                                                                                                                      |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Replication                       | Constraints on servers:                                                                                                                                                                                |
   |                                   |                                                                                                                                                                                                        |
   |                                   | -  The servers must be from two AZs of the same region.                                                                                                                                                |
   |                                   | -  The following types of servers cannot be used to create protected instances:                                                                                                                        |
   |                                   |                                                                                                                                                                                                        |
   |                                   |    -  Large Memory (Xen): This type of servers is bound to InfiniBand NICs.                                                                                                                            |
   |                                   |                                                                                                                                                                                                        |
   |                                   |    -  Disk Intensive I (Xen): This type of servers has local disks.                                                                                                                                    |
   |                                   |    -  Disk Intensive II (KVM): This type of ECSs has local disks.                                                                                                                                      |
   |                                   |                                                                                                                                                                                                        |
   |                                   |    .. note::                                                                                                                                                                                           |
   |                                   |                                                                                                                                                                                                        |
   |                                   |       You can create a replication pair using Available, shared disks and attach the replication pair to protected instances.                                                                          |
   |                                   |                                                                                                                                                                                                        |
   |                                   |       A replication pair consisting of shared disks can be attached to multiple protected instances.                                                                                                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   |                                   | Constraints on EVS disks:                                                                                                                                                                              |
   |                                   |                                                                                                                                                                                                        |
   |                                   | -  Disks used to create replication pairs cannot be deleted, and the disk snapshot cannot be used to roll back data.                                                                                   |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Storage                           | This service is applicable for servers using only EVS.                                                                                                                                                 |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Application                       | Storage-based synchronous replication ensures disk data consistency but cannot ensure application consistency. If your applications support crash consistency, you can run and replicate applications. |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Deployment model                  | **VPC migration**: Servers at the production site and those at the DR site are in the same VPC. NIC migration and multiple NICs are supported for each server.                                         |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Backup and restoration            | Only servers at the production site can be backed up and restored. Servers at the DR site can only be backed up.                                                                                       |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   If the AZ of the production site becomes faulty, you can use the DR drill function to restore the server services in the AZ.

Constraints on Logging In to the Server After a Switchover, Failover, or DR Drill Is Executed First Time Ever
-------------------------------------------------------------------------------------------------------------

-  After you have performed a switchover, failover, or DR drill for the first time:

   If your servers are installed with Cloud-Init/Cloudbase-Init, Cloud-Init/Cloudbase-Init will start along with the server's first startup to inject the initial data. In this case, the password or key pair used to log in to the production site server, DR site server, or drill server will change.

-  If your servers are not installed with Cloud-Init/Cloudbase-Init, the password or key pair used to log in to the production site server, DR site server, or drill server will not change.

The following uses a switchover or failover as the example operation. For the login constraints on drill servers, see those for DR site servers.

In the following example, Server A and server B are deployed. :ref:`Table 2 <en-us_topic_0110981899__table92017496206>` shows the servers before and after the operation.

.. _en-us_topic_0110981899__table92017496206:

.. table:: **Table 2** Servers before and after a switchover or failover

   ====== ====================== ==============
   N/A    Production Site Server DR Site Server
   ====== ====================== ==============
   Before A                      B
   After  B                      A
   ====== ====================== ==============

Detailed login constraints are described as follows:

**Scenario 1**: Server A runs Windows and does not have Cloudbase-Init installed. After the first time switchover or failover:

-  If your servers use password for login, you can use the password of Server A to log in to the production site server (Server B) or DR site server (Server A).
-  If your servers use key pair for login, you can use the obtained password of Server A to log in to the production site server (Server B) or DR site server (Server A).

.. note::

   After the first time switchover or failover, the password or key pair remains the same for the subsequent switchovers or failovers. Take servers listed in :ref:`Table 2 <en-us_topic_0110981899__table92017496206>` as an example.

   You can use the password of Server A to log in to the production site server or DR site server.

**Scenario 2**: Server A runs Windows and already has Cloudbase-Init installed. After the first time switchover or failover:

-  When your servers use password for login,

   If Cloudbase-Init is not started (normally within 3 to 5 minutes after the production site server starts), you can use the password of Server B for login.

   After Cloudbase-Init is started, the login password of Server B becomes invalid. Reset the password and use the new password for login.

-  When your servers use key pair for login,

   If Cloudbase-Init is not started (normally within 3 to 5 minutes after the production site server starts), you can use the obtained login password of Server B for login.

   After Cloudbase-Init is started, the obtained login password of Server B becomes invalid. Obtain the password again.

.. note::

   After the first time switchover or failover, the password or key pair remains the same for the subsequent switchovers or failovers. Take servers listed in :ref:`Table 2 <en-us_topic_0110981899__table92017496206>` as an example.

   -  Login using a password: Reset the password of Server B and use the new password for login.
   -  Login using a key pair: Obtain the password of Server B again and use the obtained password to log in to Server B.

**Scenario 3**: Server A runs Linux. After the first time switchover or failover:

-  If your servers use password for login, you can use the password of Server A to log in to the production site server (Server B) or disaster recovery site server (Server A). Specifically:

   If the login password of Server A is not changed before the operation, use this password for login.

   If the login password of server A has been changed before the operation, use the new password for login.

   .. note::

      For ECS OSs other than CoreOS, the login password does not change after the first time switchover or failover.

      For ECSs running CoreOS, the login password of Server A will restore to the initial one after the first time switchover or failover. In this case, use the login password configured when Server A is created to log in to production site Server A or DR site Server B.

-  If your server uses key pair for login, use the SSH key pair of Server A to log in to production site Server B or DR site Server A.
