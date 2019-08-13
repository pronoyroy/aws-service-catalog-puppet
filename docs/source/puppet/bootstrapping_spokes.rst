Bootstrapping Spoke Accounts
============================

.. contents:: Table of Contents
   :depth: 1
   :local:

What is Bootstrapping and How do I do it?
----------------------------------------

In the previous sections you setup your Puppet Account so that you could centrally manage the sharing of Portfolio and launch of Products across other Accounts in your estate.

To enable Puppet to interact with other Accounts (called Spoke Accounts throughout the documentation) in your estate we need to bootstrap them with a new IAM Role which can be assumed (via a Trust) by the Puppet Account. This Role has the permissions required to Manage the Portfolios and launch the Products in that Account.

There are 2 methods of bootstrapping available:

**METHOD 1**

Export IAM creadentials for an existing Spoke Account and run from the command live within your virtualenv:

.. code-block:: bash

    servicecatalog-puppet bootstrap-spoke <12_DIGIT_ID_OF_THE_PUPPET_ACCOUNT>

**METHOD 2**

Make use of the `Account Vending Machine`__ Product as this allows you to create AWS Accounts and bootstrap them with the PuppetRole. Note that this requires you to be using AWS organizations.

.. Add Links below. They are in the order in which they are used.

.. _AVM: https://github.com/awslabs/aws-service-catalog-products
__ AVM_