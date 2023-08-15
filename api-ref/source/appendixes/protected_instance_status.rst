:original_name: en-us_topic_0126152931.html

.. _en-us_topic_0126152931:

Protected Instance Status
=========================

+-----------------------------------+--------------------------------------------------------------------------------------------+
| Protected Instance Status         | Description                                                                                |
+===================================+============================================================================================+
| creating                          | The protected instance is being created.                                                   |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| available                         | The protected instance is available.                                                       |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| deleting                          | The protected instance is being deleted.                                                   |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error-deleting                    | Failed to delete the protected instance.                                                   |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error                             | Failed to create the protected instance.                                                   |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| nic-creating                      | The system is adding a NIC to the protected instance.                                      |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| nic-deleting                      | The system is deleting a NIC from the protected instance.                                  |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| starting                          | Protection is being enabled for the protected instance.                                    |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error-starting                    | Failed to enable protection for the protected instance.                                    |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| protected                         | Protection is enabled for the protected instance.                                          |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| reversing                         | The system is performing a planned failover for the protected instance.                    |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| failing-over                      | The system is performing a failover for the protected instance.                            |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| failed-over                       | A failover is performed for the protected instance.                                        |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| reprotecting                      | Protection is being enabled again for the protected instance.                              |
|                                   |                                                                                            |
|                                   | When users enable protection after a failover, the status changes to re-protecting.        |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| stopping                          | Protection is being disabled for the protected instance.                                   |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error-stopping                    | Failed to disable protection for the protected instance.                                   |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error-reversing                   | Failed to perform the planned failover for the protected instance.                         |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error-failing-over                | Failed to perform the failover for the protected instance.                                 |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error-reprotecting                | Failed to enable protection again for the protected instance.                              |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| resizing                          | The specifications of the protected instance are being modified.                           |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| error-resizing                    | Failed to modify the specifications of the protected instance.                             |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| invalid                           | A server in the protected instance has been deleted.                                       |
+-----------------------------------+--------------------------------------------------------------------------------------------+
| fault                             | The synchronization status of the replication pair for the protected instance is abnormal. |
+-----------------------------------+--------------------------------------------------------------------------------------------+
