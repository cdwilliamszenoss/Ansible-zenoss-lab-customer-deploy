
Control Center / Resource Manager

5.x.x and 6.x.x Zenoss Resource Manager.

Reqirements:

- SSH PUBLIC KEY AUTHENTICATION required for installation. (You should be able to connect to server via ssh without a password)

- Downloaded files listed in files-required-site-[5-6].txt. Save the files to zenoss-lab-customer-deploy/common/files/install directory 

- Server with Centos 7.4 OS

- Second hard drive or (3) partitions for the installation. 


----

Step 1. 

Download repository to workstation. 

Example:

git clone https://github.com/cdwilliamszenoss/zenoss-lab-customer-deploy.git

Install ansible on workstation.

Example:

yum install ansible

----

Step 2.

Default : Using the script to create partitions. 

Modify the site-6.1.1.yml or site-5.3.3.yml 
- Set the harddrive device name

optional:

Set partition creation size.

optional:

Set partiton ID to use for specific service. 

Note: Use existing partitions. 

First, comment the following lines in the zenoss-lab-customer-deploy/common/tasks/main.yml with #  
\- name: Delete partitions\
  include: delete_partitions.yml

\- name: Create partitions\
  include: create_partitions.yml

Second, modify the site-6.1.1.yml or site-5.3.3.yml 
- Set the harddrive device name and partition ID where each service will be installed.

 
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
     
     This script will NOT UPGRADE an existing installation.



