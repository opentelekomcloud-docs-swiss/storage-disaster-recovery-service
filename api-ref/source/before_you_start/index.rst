:original_name: sdrs_01_0001.html

.. _sdrs_01_0001:

Before You Start
================

Overview
--------

Welcome to the . provides cross-AZ disaster recovery (DR) for cloud servers with zero RPO. It simplifies the DR process and can greatly reduce the DR TCO for enterprises. If a fault occurs at the production site, you can quickly restore services at the DR site. This significantly shortens the service downtime and reduces the loss.

This document describes how to use application programming interfaces (APIs) to perform operations on protection groups, protected instances, and replication pairs, and perform DR drills. For details about all supported operations, see :ref:`API Overview <sdrs_02_0000>`.

If you plan to use SDRS through APIs, ensure that you are familiar with SDRS concepts. For details, see section "Service Overview" of the Storage Disaster Recovery Service.

API Calling
-----------

supports Representational State Transfer (REST) APIs, allowing you to call APIs using HTTPS. For details about API calling, see :ref:`Calling APIs <sdrs_03_0000>`.

Endpoints
---------

An endpoint is the **request address** for calling an API. Endpoints vary depending on services and regions. For the endpoints of all services, see `Regions and Endpoints <https://docs.sc.otc.t-systems.com/en-us/endpoint/index.html>`__.

Constraints
-----------

-  The number of resources that you can create is determined by your quota. To view or increase the quota, see section "Managing Quotas" in the *User Guide*.
-  For detailed constraints, see the constraints described in specific APIs.

Concepts
--------

-  Domain

   A domain has full access permissions for all of its cloud services and resources. It can be used to reset user passwords and grant user permissions. The domain should not be used directly to perform routine management. For security purposes, create Identity and Access Management (IAM) users and grant them permissions for routine management.

-  User

   An IAM user is created by an account in IAM to use cloud services. Each IAM user has its own identity credentials (password and access keys).

   API authentication requires information such as the domain name, username, and password.

-  Region

   A region is a geographic area in which cloud resources are deployed. Availability zones (AZs) in the same region can communicate with each other over an intranet, while AZs in different regions are isolated from each other. Deploying cloud resources in different regions can better suit certain user requirements or comply with local laws or regulations.

-  AZ

   An AZ comprises of one or more physical data centers equipped with independent ventilation, fire, water, and electricity facilities. Computing, network, storage, and other resources in an AZ are logically divided into multiple clusters. AZs within a region are interconnected using high-speed optical fibers to allow you to build cross-AZ high-availability systems.

-  Project

   A project corresponds to a region. Default projects are defined to group and physically isolate resources (including computing, storage, and network resources) across regions. Users can be granted permissions in a default project to access all resources under their domains in the region associated with the project. If you need more refined access control, create subprojects under a default project and create resources in subprojects. Then you can assign users the permissions required to access only the resources in the specific subprojects.


   .. figure:: /_static/images/en-us_image_0000001924299688.png
      :alt: **Figure 1** Project isolation model

      **Figure 1** Project isolation model

-  :ref:`Overview <sdrs_01_0000>`
-  :ref:`API Calling <sdrs_01_0002>`
-  :ref:`Endpoints <sdrs_01_0003>`
-  :ref:`Constraints <sdrs_01_0004>`
-  :ref:`Concepts <sdrs_01_0005>`

.. toctree::
   :maxdepth: 1
   :hidden: 

   overview
   api_calling
   endpoints
   constraints
   concepts
