:original_name: en-us_topic_0126152932.html

.. _en-us_topic_0126152932:

Replication Pair Status
=======================

+-----------------------------------+-------------------------------------------------------------------------------------+
| Replication Pair Status           | Description                                                                         |
+===================================+=====================================================================================+
| creating                          | The replication pair is being created.                                              |
+-----------------------------------+-------------------------------------------------------------------------------------+
| available                         | The replication pair is available.                                                  |
+-----------------------------------+-------------------------------------------------------------------------------------+
| deleting                          | The replication pair is being deleted.                                              |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-deleting                    | Failed to delete the replication pair.                                              |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error                             | Failed to create the replication pair.                                              |
+-----------------------------------+-------------------------------------------------------------------------------------+
| extending                         | The system is expanding the capacity of the replication pair.                       |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-extending                   | Failed to expand the capacity of the replication pair.                              |
+-----------------------------------+-------------------------------------------------------------------------------------+
| starting                          | The system is enabling protection for the replication pair.                         |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-starting                    | Failed to enable protection for the replication pair.                               |
+-----------------------------------+-------------------------------------------------------------------------------------+
| protected                         | Protection is enabled for the replication pair.                                     |
+-----------------------------------+-------------------------------------------------------------------------------------+
| reversing                         | The system is performing a planned failover for the replication pair.               |
+-----------------------------------+-------------------------------------------------------------------------------------+
| failing-over                      | The system is performing a failover for the replication pair.                       |
+-----------------------------------+-------------------------------------------------------------------------------------+
| failed-over                       | Failover is performed for the replication pair.                                     |
+-----------------------------------+-------------------------------------------------------------------------------------+
| reprotecting                      | The system is enabling protection again for the replication pair.                   |
|                                   |                                                                                     |
|                                   | When users enable protection after a failover, the status changes to re-protecting. |
+-----------------------------------+-------------------------------------------------------------------------------------+
| stopping                          | The system is disabling protection for the replication pair.                        |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-stopping                    | Failed to disable protection for the replication pair.                              |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-reversing                   | Failed to perform a planned failover for the replication pair.                      |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-failing-over                | Failed to perform a failover for the replication pair.                              |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-reprotecting                | Failed to enable protection again for the replication pair.                         |
+-----------------------------------+-------------------------------------------------------------------------------------+
| invalid                           | A disk in the replication pair has been deleted.                                    |
+-----------------------------------+-------------------------------------------------------------------------------------+
| fault                             | The synchronization status of the replication pair is abnormal.                     |
+-----------------------------------+-------------------------------------------------------------------------------------+
| attaching                         | The system is attaching the replication pair to a protected instance.               |
+-----------------------------------+-------------------------------------------------------------------------------------+
| detaching                         | The system is detaching the replication pair from a protected instance.             |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-attaching                   | Failed to attach the replication pair to a protected instance.                      |
+-----------------------------------+-------------------------------------------------------------------------------------+
| error-detaching                   | Failed to detach the replication pair from a protected instance.                    |
+-----------------------------------+-------------------------------------------------------------------------------------+
