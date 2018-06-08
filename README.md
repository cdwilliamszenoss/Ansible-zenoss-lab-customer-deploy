
Control Center / Resource Manager

5.x.x and 6.x.x Zenoss Resource Manager.

Reqirements:

SSH PUBLIC KEY AUTHENTICATION required for installation. (connect to server via ssh from ansible managment workstation)

Installation files downloaded from Zenoss. Listed in files-required-site-[5-6].txt  

Server with Centos 7.4 OS

Second drive for Zenoss installation. 

Update site-configuration in site-6.1.1.yml or site-5.3.3.yml.

----

Step 1. 

Download repository to workstation. 

Example:

git clone git@github.com:cdwilliamszenoss/zenoss-lab-customer-deploy.git


Install ansible on workstation.

Example:

yum install ansible

----

Step 2.

Modify the site-6.1.1.yml or site-5.3.3.yml to update DNS ip address, harddrive name for Zenoss installation.

optional:

Set partition creation size.

optional:

Set partiton ID to use for specific service. 
 
----

Step 3.

Update hosts (FQDN) name in inventory file (located in repository directory downloaded on workstation).

Example:

vi $PATH/zenoss-lab-customer-deploy/hosts

lab107.zenoss.sup

----

Step 4.

Copy files listed in files-required-site-5.txt or files-required-site-6.txt to the install directory.
(located in repository directory downloaded on workstation)

$PATH/zenoss-lab-customer-deploy/common/files/install 

----

Step 5.

Select the version of Zenoss to install

Example:

ansible-playbook -i hosts site-5.3.3.yml

or

Example:

ansible-playbook -i hosts site-6.1.1.yml


Important Note:
     DO NOT USE ON YOUR EXISTING INSTANCES.
     
     New installs only. Will NOT UPGRADE an existing installation.
     It will delete all partitions on xvdb. 



