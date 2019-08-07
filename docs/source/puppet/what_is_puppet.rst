What is Service Catalog Puppet?
===============================

**Service Catalog Puppet** is an Open Source framework which allows you to provision AWS Service
Catalog Products into multiple Accounts and Regions across your AWS Estate.

The Tool builds upon the features provided by the native AWS Service Catalog Service including:

- Adding Multi Region Portfolio sharing
- Adding a Multi Account Hub and Spoke sharing model for Portfolios
- Adding a Multi Account Hub and Spoke provisioning model for Products

The Tool reduces the Operational burden of engineering a solution to support Product Provisioning 
across a large Enterprise and allows you to focus on writing the Products you require to support 
your Organizations needs.

How does Service Catalog Puppet Work?
-------------------------------------
User interaction with the Framework is via a YAML file with examples being provided throughout the proceeding documentation. The YAML file is used to describe your AWS Accounts as:

- Individual AWS Account Ids
- A List of AWS Account IDs
- A set of AWS Accounts under a given AWS Organizational OU path

The Descriptions of those Accounts can then be tagged and used to 'Share' Portfolios and 'Launch' Products into them. The initial creation of the Portfolios and products can either be done manually or using the `Service Catalog Factory Toolset`__

Under the covers, Service Catalog Puppet is converting requests into a workflow which is executed in your AWS Account using AWS CodePipeline, AWS CodeBuild and AWS CloudFormation.

High-Level Architecture Diagram
-------------------------------
.. image:: ./diagrams/whatisthis.png

You use an AWS CodeBuild project in a central _hub_ account that provisions AWS
Service Catalog Products into _spoke_ accounts on your behalf.  The framework
takes care of cross account sharing and cross region product replication for
you.

.. Add Links below. They are in the order in which they are used.

.. _SC-F: https://aws-service-catalog-factory.readthedocs.io/en/latest/index.html

__ SC-F_