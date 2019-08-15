Bootstrapping for AWS Organization Support
==========================================

.. contents:: Table of Contents
   :depth: 1
   :local:

Bootstrapping the Org Master and Puppet Account
-----------------------------------------------

If you would like to describe your AWS Accounts using an AWS Organizational Unit Path, then you will need to bootstrap both the Organization Master Account and the Puppet Account.

Bootstrapping Your Org Master Account
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bootstrapping the Org Master creates a Role which trusts the Puppet Account. This Role has Access to Read the Org Structure and list the Accounts within it.

From your virtualenv command line using IAM Credentials for the Org Master run:

.. code-block::

    servicecatalog-puppet bootstrap-org-master <ACCOUNT_ID_OF_PUPPET_ACCOUNT>

You will see a new Role get created in the Master Account. Copy the ARN of that Role as it is required for the next step

Bootstrapping Your Puppet Account
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bootstrapping the Puppet Account creates a Systems Manager Parameter which references the ARN of the role to be assumed in the Organization Master Account

.. code-block:: bash

    servicecatalog-puppet set-org-iam-role-arn <THE_ARN_OF_THE_ROLE_IN_MASTER>

.. Add Links below. They are in the order in which they are used.