
Control Center / Resource Manager

5.x.x and 6.x.x Zenoss Resource Manager.

Reqirements:

- SSH PUBLIC KEY AUTHENTICATION required for installation. (You should be able to connect to the server via ssh without a password)

- Downloaded files listed in files-required-site-[5-6].txt. Save the files to zenoss-lab-customer-deploy/common/files/install directory 

- Server with Centos 7.4 OS

- Default lab installation: Will create partitions on hard-drive with an MSDOS Partition Table (create partitions beginning at 24GB).  

- ( Work In Progress: Second hard drive or (3) partitions for the installation. )


NOTE:

- This script will also install a Zenoss HA Cluster ( look at inventory hosts file).   

----

Step 1. 

Download repository to workstation. 

Example:

git clone https://github.com/cdwilliamszenoss/zenoss-lab-customer-deploy.git

Install ansible on workstation.

Example:

yum -y install ansible

----

Step 2.

Default : Using the script to create partitions. 

Modify the site-6.1.1.yml or site-5.3.3.yml 
- Set the harddrive device name

optional:

- Set partition size. (Use the offset to determine start/end of partition)

 
----

Step 3.

Add the hostname (FQDN) to inventory file hosts file (in downloaded repository directory).

Example:

vi $PATH/zenoss-lab-customer-deploy/hosts

[standalone]

example1.somedomain.com 

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



