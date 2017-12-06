![alt text](https://github.com/Pivotal-Data-Engineering/gemfire-azure/blob/master/Pivotal-GemFire-Logo-FullColor.png)
## Pivotal GemFire On Microsoft Azure.

##### Automated provisioning of Pivotal GemFire clusters on the Microsoft Azure cloud
Currently supports GemFire version 9.1.0 

## Overview
The file _mainTemplate.json_ can be deployed using the Azure portal directly.

This project also provides a command line deployment script, _deploy.py_. See
below for details.

__Note on SSH key:__ If using the Azure portal to deploy this template, provide
the key material for the _sshPublicKey_ parameter. Provide the entire
contents of a ".pub" file generated by ssh-keygen.  For example, you could use
_~/.ssh/id\_rsa.pub_.  If you are using the _deploy.py_ script, provide the
file name for the value of the_--public-ssh-key-file_ parameter.

## Usage Example
First complete _Setup for Script Based Deployment_ (below).

The example below shows deploying a cluster into a newly created resource group with
passwordless authentication enabled on the deployed servers.

```
python deploy.py   --create-resource-group=test --resource-group-location=eastus2 --resource-location=eastus2 --admin-username=gfadmin --public-ssh-key-file=azuredev.pub --datanode-count=3
```

This example shows deploying a cluster into an existing resource group with
password authentication enabled on the deployed servers.

```
python deploy.py   --use-resource-group=test --resource-location=eastus2 --admin-username=gfadmin --public-ssh-key-file=azuredev.pub --datanode-count=3
```

The template returns the information you need to connect to your cluster.

## Setup for Script Based Deployment
Install the [Azure CLI version 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest).  
Ensure that the `az` command is on the path.

Make sure you have authenticated with the CLI: `az login`


## Developer Notes
A 3 node Vagrant development environment has been included for testing the
initialization scripts.  To test, run `vagrant up`.  The VMs will be provisioned
and the bootstrap will run providing a (somewhat) realistic simulation of the
Azure environment.  To re-run the setup scripts without re-provisioning the virtual
machines, run 'vagrant reload --provision'.

## Testing
Once the vms are provisioned, the remainder of the cluster initialization
process is handled by downloading a copy of this repository from github and
running the scripts in the _init\_scripts_ folder.

To test,before cutting a release, use the following procedure:
* commit your changes on __on a branch__ and git push them to github
* deploy using the _deploy.py_ script, it will automatically detect the
branch you are on and use that branch to configure the remote servers.


_Pivotal Gemfire is a licenced Trademark © 2017 Pivotal Software, Inc. All Rights Reserved._
_Microsoft Azure is a licenced trademark of © 2017 Microsoft corporation. All Rights Reserved._
