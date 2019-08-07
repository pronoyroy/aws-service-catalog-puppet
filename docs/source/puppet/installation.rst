Installing Service Catalog Puppet
=================================

.. contents:: Table of Contents
   :depth: 2
   :local:

Which Account Should I use for Puppet?
--------------------------------------

**Before you install Puppet, there are a few things to be aware of:**

- Puppet needs to be installed into an AWS Account which we will be calling the **Puppet Account** throughout the Docs.
- The Puppet Account will be used to Share Portfolios and Launch Products across the rest of your AWS Accounts.
- Accounts which you want to manage with Puppet must 'Trust' the Puppet Account. This is an `AWS IAM Mechanism`__ to allow a Role in one Account to Assume a Role in another Account. Don't worry, this will be explained more a little later in the Docs.
- Puppet can be used in conjuntion with `AWS Organizations`__ to describe AWS Accounts under an Organizational Unit as opposed to individually or as a list. If this is the case, your Organization Master would also need to Trust the Puppet Account.
- We recommend that if you are using `Service Catalog Factory`__, then Puppet should use the same Account.

Which Region(s) Should I Use?
-----------------------------

**Some notes on your region choice:**

- You can choose to enable one or more Regions by adding them to a Config File (See: `Uploading Configuration File`_) and Bootstrapping Puppet (See: `Bootstrapping Puppet Account`_) again
- Not all Regions currently support the base Services required by Puppet such as CodeBuild and Codepipeline. Please check the `Region Table`__ for more information.
- Each Region will increase the Cost of Running Puppet. We recommend only configuring Regions you intend to use. It can be changed at a later date as requirements change.
- As with the Account decision above, if you are using Service Catalog Factory, we recommend using the same Regions.

Create a Python Virtual Environment
-----------------------------------
Virtual Environments allow you to manage different versions of Python and other required dependencies in isolation without affecting the running of the rest of your Applications on the same Machine. We recommend having an independent Virtual Environment for Puppet as in some cases the dependencies are at a different version to those required by tools like Service Catalog Factory (for example).

Pre-reqs to Creating a Virtual Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
To create a Virtual Environment, you must have Python3 and VirtualEnv installed on your machine.

Creating a Virtual Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: bash

    virtualenv --python=python3.7 venv

Activating a Virtual Environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: bash

    source venv/bin/activate

Install Service Catalog Puppet
------------------------------
Once you have successfully created and activated your environment, you are ready to install the Puppet Package locally to your Machine.

.. code-block:: bash
    pip install aws-service-catalog-puppet

Uploading Configuration File
----------------------------
As noted above, we use a Configuration File to define the Regions in which we want Puppet to Operate in. 

Create the Configuration File
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
This is just a json file with region names in it. Create this file in a location of your choice.

Configuration File Example:

.. code-block:: yaml

    regions: [
      'us-east-2',
      'us-east-1',
      'us-west-1',
      'us-west-2',
      'eu-west-1',
      'eu-west-2',
      'eu-west-3',
    ]

Uploading the Configuration File
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Once the file has been created, we can now upload it:

.. code-block:: bash

    servicecatalog-puppet upload-config config.yaml

Bootstrapping Puppet Account
----------------------------
Bootstrapping the Environment will setup your Puppet Account with all of the requisite AWS Services such as CodeBuild jobs and CodePipeline to enable Puppet to function

Some Considerations:

- If you make changes to your config you will need to run upload-config and bootstrap commands again for the changes to occur.
- Prior to bootstrapping, you must make sure you have setup your `AWS Credentials`__ for the Puppet Account

Once that has completed you are ready to bring up the rest of the puppet.


.. Add Links below. They are in the order in which they are used.

.. _IAM: https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-user.html
__ IAM_

.. _Org: https://aws.amazon.com/organizations/
__ Org_

.. _SC-F: https://aws-service-catalog-factory.readthedocs.io/en/latest/index.html
__ SC-F_

.. _Region: https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/
__ Region_

.. _Creds: https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html
__ Creds_








