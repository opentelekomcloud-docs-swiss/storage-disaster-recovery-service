:original_name: en-us_topic_0108180816.html

.. _en-us_topic_0108180816:

Configuration Process
=====================

SDRS provides cross-AZ server-level protection (RPO = 0) in case applications at a production site cannot restore in a short period of time caused by force majeure like fires or earthquakes or device faults like damaged software or hardware. Synchronous replication at the storage layer is used to provide cross-AZ DR protection, and thereby meeting the crash consistency of data. If the production site becomes faulty, you can rapidly restore the services at the DR site after simple configuration.

:ref:`Figure 1 <en-us_topic_0108180816__fig19593154813218>` shows the cross-AZ DR configuration process.

.. note::

   When you create a protected instance, the system creates a replication pair for the disks of the servers at the production and DR site by default.

.. _en-us_topic_0108180816__fig19593154813218:

.. figure:: /_static/images/en-us_image_0288665371.png
   :alt: **Figure 1** Cross-AZ DR configuration process

   **Figure 1** Cross-AZ DR configuration process
