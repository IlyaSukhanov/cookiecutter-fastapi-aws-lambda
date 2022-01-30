==================================
FastAPI on AWS Lambda Cookiecutter
==================================

Generate bootstrapping code and configuration for deploying and running
of FastAPI applications on AWS Lambda. In addition to the obvious FastAPI,
this project also utilized `Mangum <https://github.com/jordaneremieff/mangum>`_
to translate AWS Events to Fast API and the `Serverless <https://www.serverless.com/>`_
framework for deployment.

Quick start
------------

Project initialization:

.. code-block:: shell
    
    pip install cookiecutter
    cookiecutter https://github.com/IlyaSukhanov/cookiecutter-fastapi-aws-lambda.git

After answering prompts you'll end up with a bootstrapped project that'll similar to

.. code-block::

	.
	├── cheezoid
	│   ├── app.py
	│   ├── __init__.py
	│   └── schemas.py
	├── config
	│   └── logging.conf
	├── LICENSE
	├── Makefile
	├── pyproject.toml
	├── README.rst
	├── requirements_dev.txt
	├── requirements.txt
	├── serverless.yml
	├── setup.cfg
	└── tests
		└── test_app.py

There are several convenience make targets to ease the development workflow

 1. `make install-dev` Installs all python development dependencies
 2. `make format` Formats python code with black and isort
 3. `make test` Lint checks the code and runs unit tests

If you have not yet configured AWS Profile now is a good time to do so. Refer to
`AWS documentation <https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html>`_
for details.

This project utilizes Serveless for deployment which requires node to be installed
on the machine from which deployments will be performed. All of the subsequent steps
assume node.js is already installed.

Finally you can deploy project:

 1. `make configure-deploy` Installs serverless.js and other necessary dependencies.
    This generally only need to be performed once
 2. `make deploy-dev` Deploys application to AWS Lambda using development environment
    settings

Undo deployment:

 1. `make undeploy-dev` Removes deployment and all other resources that were created
    with deploy-dev.


Postgres
--------

This project has partial implementation to allow use of postgres libraries. This is a
more involved configuration as it requires packaging up of postgres system libraries
into the lambda artifact. When this option is enabled it introduces a dependency on
docker which is needed for the packaging. This option is to be considered experimental
as it may be rough around the edges.

Should you need include other system libraries into a you project following postgres
example should be a good starting point.
