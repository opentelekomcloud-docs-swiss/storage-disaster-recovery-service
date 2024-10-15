:original_name: en-us_topic_0110273585.html

.. _en-us_topic_0110273585:

Modifying Specifications of a Protected Instance
================================================

Scenarios
---------

If the specifications of an existing protected instance cannot meet the service requirements, you can perform steps provided in this section to modify the server specifications, including the vCPU and memory.

The following scenarios may involve:

-  Modifying the specifications of both the production and DR site servers
-  Modifying the specifications of the production site server only
-  Modifying the specifications of the DR site server only

**Prerequisites**
-----------------

-  The protection group is in the **Available** or **Protecting state**.
-  The protected instance is in the **Available**, **Protecting**, or **Modifying specifications failed**.
-  Servers of which the specifications to be modified are stopped.

Procedure
---------

#. In the pane of the protection group for which the protected instance specifications are to be modified, click **Protected Instances**.

   The operation page for the protection group is displayed.

#. On the **Protected Instances** tab, locate the row containing the target protected instance, click **More** in the **Operation** column, and choose **Modify Production Site Server Specifications** or **Modify DR Site Server Specifications** from the drop-down list.

#. In the displayed dialog box, select new server type, vCPU, and memory specifications.

#. (Optional) If you need to modify the specifications of both the production site server and DR site server, select **Modify the specifications of both the production and DR site servers**. After you select this item, the system will modify the specifications of both the production site server and DR site server to the same specifications.


   .. figure:: /_static/images/en-us_image_0000002082513289.png
      :alt: **Figure 1** Modifying the specifications of both the production site server and DR site server

      **Figure 1** Modifying the specifications of both the production site server and DR site server

   .. note::

      This item is deselected by default, indicating that the system modifies the specifications of only the production site server or DR site server.

#. Click **OK**.

   To ensure proper server running, do not perform any operations to the servers during specification modifications.

--------------

Copyright © Huawei Technologies Co., Ltd.
