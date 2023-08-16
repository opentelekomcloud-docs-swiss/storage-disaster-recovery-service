:original_name: sdrs_ug_cts_0002.html

.. _sdrs_ug_cts_0002:

Viewing Traces
==============

Scenarios
---------

After you enable CTS, the system starts recording operations on SDRS. You can view operation records of the last seven days on the management console.

Procedure
---------

#. Log in to the management console.

#. Click **Service List** and select **Cloud Trace Service** under **Management & Deployment**.

#. In the navigation pane on the left, choose **Trace List**.

#. In the upper right corner of the trace list, click **Filter** to set the search criteria.

   The following four filters are available:

   -  **Trace Source**, **Resource Type**, and **Search By**

      -  Select a filter criterion from the drop-down list. Select **SDRS** for **Trace Source**.
      -  When you select **Trace name** for **Search By**, you need to select a specific trace name.
      -  When you select **Resource ID** for **Search By**, you need to select or enter a specific resource ID.
      -  When you select **Resource name** for **Search By**, you need to select or enter a specific resource name.

   -  **Operator**: Select a specific operator (at user level rather than tenant level).
   -  **Trace Status**: Available options include **All trace statuses**, **normal**, **warning**, and **incident**. You can only select one of them.
   -  **Time Range**: You can query traces generated during any time range of the last seven days.

#. Click |image1| on the left of the required trace to expand its details.

#. Locate a trace and click **View Trace** in the **Operation** column.

.. |image1| image:: /_static/images/en-us_image_0288665363.jpg
