:original_name: sdrs_faq_0005.html

.. _sdrs_faq_0005:

What Are the Precautions If I Log In to the Production Site Server Using a Key Pair?
====================================================================================

-  If the production site server runs Windows and uses a key pair for login, ensure that the key pair exists when you create a protected instance or a DR drill. Or, the DR site server or drill server may fail to create, thus causing the creation failure of the protected instance or DR drill.
-  If the production site server runs Linux and uses a key pair for login, you can create a protected instance or DR drill regardless of whether the key pair exists or not. Key pair information will not be shown on the details page of the created DR site server or drill server. But you can use the key pair of the production site server to log in to the created DR site server and drill server.

   .. important::

      If the production site server runs Windows, uses a key pair for login, and is created by an IAM user, only that IAM user can create a protected instance for this server. Other users do not have permissions on the key pair of this server. If they create a protected instance for this server, the creation will fail.
