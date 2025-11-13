:original_name: sdrs_ug_cts_0001.html

.. _sdrs_ug_cts_0001:

Key SDRS Operations Recorded by CTS
===================================

.. table:: **Table 1** SDRS operations that can be recorded by CTS

   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Operation                                                                                              | Resource Type         | Trace Name               |
   +========================================================================================================+=======================+==========================+
   | Creating a protection group                                                                            | protectionGroup       | createProtectionGroup    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Deleting a protection group                                                                            | protectionGroup       | deleteProtectionGroup    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Updating a protection group                                                                            | protectionGroup       | updateProtectionGroup    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Enabling protection for a protection group (when the protection group is in the **Available** state)   | protectionGroup       | startProtectionGroup     |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Enabling protection for a protection group (when the protection group is in the **failed-over** state) | protectionGroup       | reprotectProtectionGroup |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Disabling protection for a protection group                                                            | protectionGroup       | stopProtectionGroup      |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Performing a failover for a protection group                                                           | protectionGroup       | failoverProtectionGroup  |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Reprotecting a protection group                                                                        | protectionGroup       | reverseProtectionGroup   |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Action performed when a job of the protection group failed to submit                                   | protectionGroup       | protectionGroupAction    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Creating a protected instance                                                                          | protectedInstance     | createProtectedInstance  |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Deleting a protected instance                                                                          | protectedInstance     | deleteProtectedInstance  |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Updating a protected instance                                                                          | protectedInstance     | updateProtectedInstance  |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Attaching a replication pair to a protected instance                                                   | protectedInstance     | attachReplicationPair    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Detaching a replication pair from a protected instance                                                 | protectedInstance     | detachReplicationPair    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Adding a NIC to a protected instance                                                                   | protectedInstance     | addNic                   |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Deleting a NIC from a protected instance                                                               | protectedInstance     | deleteNic                |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Modifying the specifications of a protected instance                                                   | protectedInstance     | resizeProtectedInstance  |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Creating a replication pair                                                                            | replicationPair       | createReplicationPair    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Deleting a replication pair                                                                            | replicationPair       | deleteReplicationPair    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Updating a replication pair                                                                            | replicationPair       | updateReplicationPair    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Expanding the capacity of a replication pair                                                           | replicationPair       | expandReplicationPair    |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Creating a DR drill                                                                                    | disasterRecoveryDrill | createDrDrill            |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Deleting a DR drill                                                                                    | disasterRecoveryDrill | deleteDrDrill            |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
   | Updating a DR drill                                                                                    | disasterRecoveryDrill | updateDrDrill            |
   +--------------------------------------------------------------------------------------------------------+-----------------------+--------------------------+
