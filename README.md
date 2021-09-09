About
=====

troposphere - library to create `AWS CloudFormation`_ descriptions

The troposphere library allows for easier creation of the `AWS CloudFormation
JSON`_ by writing Python code to describe the AWS resources. troposphere also
includes some basic support for `OpenStack resources`_ via Heat.

To facilitate catching CloudFormation or JSON errors early the library has
property and type checking built into the classes.

Installation
============

troposphere can be installed using the pip distribution system for Python by
issuing:

.. code:: sh

    $ pip install troposphere

To install troposphere with `awacs <https://github.com/cloudtools/awacs>`_
(recommended soft dependency):

.. code:: sh

    $ pip install troposphere[policy]

Alternatively, you can use `setup.py` to install by cloning this repository
and issuing:

.. code:: sh

    $ python setup.py install  # you may need sudo depending on your python installation

Examples
========

A simple example to create an instance would look like this:

.. code:: python

    >>> from troposphere import Ref, Template
    >>> import troposphere.ec2 as ec2
    >>> t = Template()
    >>> instance = ec2.Instance("myinstance")
    >>> instance.ImageId = "ami-951945d0"
    >>> instance.InstanceType = "t1.micro"
    >>> t.add_resource(instance)
    <troposphere.ec2.Instance object at 0x101bf3390>
    >>> print(t.to_json())
    {
        "Resources": {
            "myinstance": {
                "Properties": {
                    "ImageId": "ami-951945d0",
                    "InstanceType": "t1.micro"
                },
                "Type": "AWS::EC2::Instance"
            }
        }
    }
    >>> print(t.to_yaml())
    Resources:
        myinstance:
            Properties:
                ImageId: ami-951945d0
                InstanceType: t1.micro
            Type: AWS::EC2::Instance

