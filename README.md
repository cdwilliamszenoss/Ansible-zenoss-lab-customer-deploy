
Control Center / Resource Manager

5.x.x and 6.x.x Zenoss Resource Manager.

Reqirements:

- SSH PUBLIC KEY AUTHENTICATION required for installation. (You should be able to connect to the server via ssh without a password)

- Downloaded files listed in files-required-site-[5-6].txt. Save the files to zenoss-lab-customer-deploy/common/files/install directory 

- Server with Centos 7.* OS

- Default lab installation: Will create partitions on hard-drive with an MSDOS Partition Table (create partitions beginning at 54GB).  

NOTE:

- There is a new HA cluster playbook and role for setting up an HA cluster running RM 6.1.2.

- You will need to create an encrypted ansible vault file and variables file for the ha user credentials.  See the following example on how to set this up.

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

ansible-playbook -i hosts ha-site-6.1.2.yaml --ask-vault-pass

---
# STANDALONE -- INSTALL
---

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

vi $PATH/zenoss-lab-customer-deploy/hosts.example.file

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



