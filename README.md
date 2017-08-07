# packer-ami-builder
A proof of concept for building an AMI with Packer

## Requirements
* Packer

Pick your [platform
](https://www.packer.io/downloads.html "Packer")'s executable and place it in your path (e.g. `/usr/local/bin`).
**Beware**, due to an [issue](https://github.com/hashicorp/packer/issues/5142), you have to install version **1.0.2**!
* Ansible

We are using remote ansible, therefore ansible needs to be installed on the local machine. Follow the [instructions](http://docs.ansible.com/ansible/latest/intro_installation.html "Ansible").

## Local environment
* Make sure you have a ~/.aws/credentials with your keys.
* Setup a config file at ~/.aws/config with the following content:
```
[default]
region = eu-west-1

[profile developer]
role_arn=arn:aws:iam::490532000571:role/Developer
source_profile = default

[profile terraform]
role_arn=arn:aws:iam::490532000571:role/Terraformer
source_profile = default
```
* Make sure that in the local environment `AWS_PROFILE` is set to `developer` (ex: in bash `export AWS_PROFILE=developer`).

## Build the AMI
To build the flask AMI, navigatate to the project's directory and run:

`packer build flask_ami.json`

If no errrors occured, you can see the artifact created, provisioned with the test flask web server, on [AWS](https://eu-west-1.console.aws.amazon.com/ec2/v2/home?region=eu-west-1#Images:sort=name "AWS"). Do not forget to deregister the the image and delete the snaphot, after you're done with it, as per [instructions](https://www.packer.io/intro/getting-started/build-image.html "Packer instructions").
