:original_name: sdrs_ug_pi_0008.html

.. _sdrs_ug_pi_0008:

Managing Protected Instance Tags
================================

Scenarios
---------

Tags are identifiers of protected instances. You can add tags for protected instances, and classify and search the protected instances based on these tags.

You can add a maximum of 10 tags for each protected instance when creating the protected instance or add them on the details page of the created protected instance.

**Context**
-----------

A tag consists of a tag key and a tag value. :ref:`Table 1 <sdrs_ug_pi_0008__en-us_topic_0092499768_table197401426182516>` lists the tag key and value requirements.

.. _sdrs_ug_pi_0008__en-us_topic_0092499768_table197401426182516:

.. table:: **Table 1** Tag key and value requirements

   +-----------------------+---------------------------------------------------------------------------+-----------------------+
   | Parameter             | Requirement                                                               | Example               |
   +=======================+===========================================================================+=======================+
   | Tag key               | -  Cannot be left blank.                                                  | Organization          |
   |                       | -  Must be unique.                                                        |                       |
   |                       | -  Can contain a maximum of 36 characters.                                |                       |
   |                       | -  Can only consist of digits, letters, hyphens (-), and underscores (_). |                       |
   +-----------------------+---------------------------------------------------------------------------+-----------------------+
   | Tag value             | -  Can contain a maximum of 43 characters.                                | Marketing             |
   |                       | -  Can only consist of digits, letters, hyphens (-), and underscores (_). |                       |
   +-----------------------+---------------------------------------------------------------------------+-----------------------+

Procedure
---------

You can perform the following operations based on tags:

-  Adding tags for a protected instance when you create the protected instance

   For details, see :ref:`Step 2: Create a Protected Instance <en-us_topic_0110037558>`.

-  Searching for protected instances by tag on the protected instance list page

   #. Log in to the management console.

   #. Choose **Storage** > **Storage Disaster Recovery Service**.

   #. In the pane of the protection group, click **Protected Instances**.

   #. On the **Protected Instances** tab, click **Search by Tag** in the upper right corner of the protected instance list to expand the search area.

   #. Enter the tag of the protected instance to be searched.

      Both the tag key and tag value must be specified. When the tag key or tag value is matched, the system automatically shows the target protected instances.

   #. Click |image1| to add a tag.

      The system supports multiple tags and uses the intersection set of all tags to search for protected instances.

   #. Click **Search**.

      The system searches for protection instances by tags.

-  Adding, deleting, modifying, and searching for tags on the **Protected Instance Details** page

   #. Log in to the management console.

   #. Choose **Storage** > **Storage Disaster Recovery Service**.

   #. In the pane of the protection group, click **Protected Instances**.

   #. Click the **Protected Instances** tab and click the name of the specified protected instance.

      The **Protected Instance Details** page is displayed.

   #. Click the **Tags** tab and perform desired operations.

      -  View tags.

         You can view details of protected instance tags, including the number of tags and the key and value of each tag.

      -  Add a tag.

         Click **Add Tag** in the upper left corner. In the displayed dialog box, enter the key and value of the tag to be added, and click **OK**.

      -  Modify a tag.

         Locate the row containing the tag to be edited and click **Edit** in the **Operation** column. In the **Edit Tag** dialog box, change the key and value of the tag and click **OK**.

      -  Delete a tag.

         Locate the row containing the tag to be deleted and click **Delete** in the **Operation** column. In the **Delete Tag** dialog box, click **OK**.

.. |image1| image:: /_static/images/en-us_image_0288665304.png
