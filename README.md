
Control Center / Resource Manager Installataion Tool

5.x.x and 6.x.x Zenoss Resource Manager.

Reqirements:

- Install Ansible on workstation ( Linux/RedHat workstation)

- SSH PUBLIC KEY AUTHENTICATION required for installation. (You should be able to connect to the server using ssh without a password)

- Clone repository to local workstation.  

- Downloaded files listed in files-required-site-[5-6].txt from Zenoss. Copy installation files to the zenoss-lab-customer-deploy/common/files/install/ directory 

- Server with RedHat/Centos 7.* OS

- Default lab installation: Will create partitions on hard-drive with an MSDOS Partition Table (create partitions beginning at 54GB).  

NOTE:

- There is a new HA cluster playbook and role for setting up an HA cluster running RM 6.1.2.

- You will need to create an encrypted ansible vault file and variables file for the ha user credentials.  See the following example on how to set this up.


---
# STANDALONE -- INSTALL
---

Step 1. 

Install Anisble:

yum -y install ansible


Step 2.

Generate SSH Key without a password on workstation for user. Accept defaults:

ssh-keygen


Step 3.

Clone repository to workstation:

git clone https://github.com/cdwilliamszenoss/zenoss-lab-customer-deploy.git


Step 4.

Copy files listed in files-required-site-5.txt or files-required-site-6.txt to the install directory.
(located in cloned repo on workstation)

$PATH/zenoss-lab-customer-deploy/common/files/install 


Step 5.

Select the version of Zenoss to install

Example:

ansible-playbook -i hosts.example.file site-5.3.3.yml

or

ansible-playbook -i hosts.example.file site-6.4.0.yml


Step 6.

Modify the playbook and set drive where Zenoss will be installed. Edit the site-6.1.1.yml or site-5.3.3.yml and set the harddrive device name.

Example: set name of device for Zenoss install 

hd_device: xvda


optional:

- Set partition size. (Use the offset to determine start/end of partition)

 
Step 7.

Modify the inventory file hosts file and set the hostname and IP address of server. Edit the [standalone] group section 

Example:

vi $PATH/zenoss-lab-customer-deploy/hosts.example.file

[standalone]

example1.somedomain.com 

----


Important Note:
     
     This script will NOT UPGRADE an existing installation.




---
# HA -- INSTALL
---
Step 1.

Ansible Vault Configuration:

- Create the vault within the zenoss-lab-customer-deploy directory:

Example:

ansible-vault create .vault

- Enter the desired .vault password

---
Step 2.

- Create a variables file that contains the ha user's credentials in 'key: value' format:

Example:

vi cluster/vars/secrets.yml

hapassword: "superSekretPassword"

---
Step 3.

- Encrypt the secrets.yml file with your ansible vault

Example:

ansible-vault encrypt cluster/var/secrets.yml

- When prompted, enter the .vault password specified in Step 1.

---
Step 4.

- Use the '--ask-vault-pass' option when running your playbook to decrypt the secret.yml variables for use in your playbook.

Example:

ansible-playbook -i hosts.example.file ha-site-6.1.2.yaml --ask-vault-pass



