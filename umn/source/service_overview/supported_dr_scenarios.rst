:original_name: sdrs_pro_0008.html

.. _sdrs_pro_0008:

Supported DR Scenarios
======================

Production Site Is Faulty
-------------------------

-  Description

   The production site has a fault. Services at the production site are affected and cannot be restored using the failover function.


   .. figure:: /_static/images/en-us_image_0288665307.png
      :alt: **Figure 1** Production site being faulty

      **Figure 1** Production site being faulty

-  Solution

   You can use the DR drill function to create DR drill servers at the DR site to resume the services.

   For more information about the DR drill function, see :ref:`Performing a DR Drill <en-us_topic_0122528555>`.

DR Site Is Faulty
-----------------

-  Description

   The DR site has a fault. Services at the production site are not affected, but a switchover cannot be performed.


   .. figure:: /_static/images/en-us_image_0288665264.png
      :alt: **Figure 2** DR site being faulty

      **Figure 2** DR site being faulty

-  Solution

   Contact to obtain technical support.

Replication Link Is Faulty
--------------------------

-  Description

   The replication link between the production site and DR site becomes faulty. Services at the production site are not affected, but a switchover cannot be performed.


   .. figure:: /_static/images/en-us_image_0288665385.png
      :alt: **Figure 3** Replication link being faulty

      **Figure 3** Replication link being faulty

-  Solution

   You do not need to perform any operations. The DR protection will automatically restore once the replication link fault is rectified.

Storage Resource at the Production Site Is Faulty
-------------------------------------------------

-  Description

   Services at the production site are affected because the storage resource at the production site has a fault.


   .. figure:: /_static/images/en-us_image_0288665263.png
      :alt: **Figure 4** Storage resource at the production site is faulty

      **Figure 4** Storage resource at the production site is faulty

-  Solution

   Use the failover function to start resources such as servers and disks at the DR site to resume the services.

   For more information about the failover function, see :ref:`Performing a Failover <en-us_topic_0108560208>`.

Storage Resource at the DR Site Is Faulty
-----------------------------------------

-  Description

   The storage resource at the DR site has a fault. Services at the production site are not affected, but a switchover or failover cannot be performed.


   .. figure:: /_static/images/en-us_image_0288665319.png
      :alt: **Figure 5** Storage resource at the DR site being faulty

      **Figure 5** Storage resource at the DR site being faulty

-  Solution

   Contact to obtain technical support.
