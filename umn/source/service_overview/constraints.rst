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

Restrictions on Logging In to a Server After You Perform a Planned Failover, Failover, or DR Drill for the First Time
---------------------------------------------------------------------------------------------------------------------

-  For servers with Cloud-Init/Cloudbase-Init installed, after you perform a planned failover, failover, or DR drill for the first time, Cloud-Init/Cloudbase-Init will start when the servers start for the first time to inject the initial data. The password or key pair for logging in to the production site server, DR site server, or DR drill server will change.
-  For servers without Cloud-Init/Cloudbase-Init installed, the password or key pair for logging in to the production site, DR site server, or DR drill server will not change after you perform a planned failover or failover for the first time.

The following describes an example of server login restrictions after you perform a planned failover or failover for the first time. For details about the login restrictions for the DR drill server, see the login restrictions for the DR site server in this scenario.

Server A and server B are deployed. After the first time planned failover or failover, the production site server and DR site server are listed in :ref:`Table 2 <en-us_topic_0110981899__table92017496206>`.

.. _en-us_topic_0110981899__table92017496206:

.. table:: **Table 2** Production site and DR site servers after a planned failover or failover

   ====== ====================== ==============
   N/A    Production Site Server DR Site Server
   ====== ====================== ==============
   Before A                      B
   After  B                      A
   ====== ====================== ==============

In this case, the detailed login restrictions are as follows:

Scenario 1: Server A runs Windows and does not have Cloudbase-Init installed. After the first time planned failover or failover:

-  If you choose to use a password for the server login, use the password of server A to log in to the production site server B or DR site server A.
-  If you choose to use a key pair for the server login, use the password obtained from server A to log in to the production site server B or DR site server A.

.. note::

   From the second time planned failover or failover, the login password or key pair of the server without Cloudbase-Init installed will remain the same. Take servers listed in :ref:`Table 2 <en-us_topic_0110981899__table92017496206>` as an example.

   You can use the password of server A to log in to the production site server or DR site server.

Scenario 2: Server A runs Windows and already has Cloudbase-Init installed. After the first time planned failover or failover:

-  If you choose to use a password for the server login, check whether Cloudbase-Init is started.

   If Cloudbase-Init is not started (normally within three to five minutes after the production site server starts), you can use the password of server B for the login.

   After the Cloudbase-Init is started, the login password of server B set before the planned failover or failover becomes invalid. You need to reset the login password of server B and then use the new password to log in to server B.

-  If you choose to use a key pair for the server login, check whether Cloudbase-Init is started.

   If Cloudbase-Init is not started (normally within three to five minutes after the production site server starts), you can use the password of server B for the login.

   After the Cloudbase-Init is started, the login password of server B obtained before the planned failover or failover becomes invalid. You need to obtain the login password of server B again.

.. note::

   From the second time planned failover or failover, the login password or key pair of the server with Cloudbase-Init installed will remain the same. Take servers listed in :ref:`Table 2 <en-us_topic_0110981899__table92017496206>` as an example.

   -  Login using a password: Reset the password of server B and use the new password to log in to server B after the first time planned failover or failover.
   -  Login using a key pair: Obtain the password of server B and use the obtained password to log in to server B after the first time planned failover or failover.

Scenario 3: Server A runs Linux. After the first time planned failover or failover:

-  If you choose to use a password for the server login, use the password of server A to log in to the production site server B or DR site server A.

   If the login password of server A is not changed before the planned failover or failover, use the login password configured when server A is created after the planned failover or failover.

   If the login password of server A is changed before the planned failover or failover, use the new login password after the planned failover or failover.

   .. note::

      For ECSs running OSs other than CoreOS, the login password does not change after the first-time planned failover or failover.

      For ECSs running CoreOS, the login password of server A will restore to the initial one after the first-time planned failover or failover. Therefore, you need to use the login password configured when server A is created to log in to production site server A or DR site server B.

-  If you choose to use a key pair for the server login, use the key pair of server A to log in to the production site server B or DR site server A in SSH mode.
