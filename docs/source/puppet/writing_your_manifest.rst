Writing your manifest
=======================

.. contents:: Table of Contents
   :depth: 1
   :local:

Purpose of the manifest file
----------------------------

The Manifest file is used to describe your AWS Accounts and define which ones you want to share portfolios and launch products into. It is possible to use AWS Organizations to make your manifest file more concise and easier to work with but the premise is the same - it is just a list of accounts and AWS Service Catalog products.

Describing Your Accounts
---------------------------

There are 2 ways to describe your Accounts in the Manifest:

- Individual AWS Account Ids
- A set of AWS Accounts under a given AWS Organizational OU Path

Using Individual AWS Account Ids
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: yaml

  schema: puppet-2019-04-01
  accounts:
    - account_id: '<YOUR_FIRST_ACCOUNT_ID>'
      name: '<MY_FIRST_ACCOUNT>'
      default_region: eu-west-1
      regions_enabled:
        - eu-west-2
        - us-east-1
      tags:
        - type:prod
        - partition:eu
        - scope:bus_app_01
    - account_id: '<YOUR_SECOND_ACCOUNT_ID>'
      name: '<MY_SECOND_ACCOUNT>'
      default_region: eu-west-1
      regions_enabled:
        - eu-west-2
        - us-east-1
      tags:
        - type:prod
        - partition:eu
        - scope:bus_app_02

Using OU Path
^^^^^^^^^^^^^

.. code-block:: yaml

  schema: puppet-2019-04-01
  accounts:
    - ou: /bus_app_01/Production
      name: 'Production Business App01'
      default_region: eu-west-1
      tags:
        - type:bus_app_01-prod
        - patchwindow:weekend

    - ou: /Department_01
      name: 'Department Apps'
      default_region: eu-west-1
      tags:
        - type:dept01-all
        - patchwindow:evenings

.. Note:: 

  OU Paths are Case Sensitive and therefore must match exactly as written in AWS Organizations

Describing Your Launches
------------------------

A Launch definition essentially tells Puppet which products to provision in which Accounts. There are 2 options to do this:

- Launch Based on Account Id
- Launch Based on Tag

Launch Based on Account Id
^^^^^^^^^^^^^^^^^^^^^^^^^^

The below code block provides an example of describing a launch of v1 of an example Product into your default region based on the 12 digit account id.

.. code-block:: yaml

  schema: puppet-2019-04-01

  launches:
    my-first-launch-example:
      portfolio: example-portfolio-name
      product: example-product-name
      version: v1
      deploy_to:
        accounts:
          - account_id: '012345678910'
          regions: defualt_region

.. note::

  The Portfolio and Product names must match exactly what is in Service Catalog

Launch Based on Tag
^^^^^^^^^^^^^^^^^^^

The below code block provides an example of describing the same launch as above of v1 of an example Product into your default region. However, this time we have used a Tag.

.. code-block:: yaml

  schema: puppet-2019-04-01
  
  launches:
    my-first-launch-example:
      portfolio: example-portfolio-name
      product: example-product-name
      version: v1
      deploy_to:
        tags:
          - tag: type:dept01-all
          regions: defualt_region
.. note::

  Note that the Tag matches one from our Account List Description earlier in this section