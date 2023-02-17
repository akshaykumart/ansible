# Ansible

Configuration management using ansible.

This page will include the steps to automate the installations of required packages and deploying django application into a remote machine

Refer https://github.com/akshaykumart/Django.git for souce code for django application
Refer https://github.com/akshaykumart/gunicorn.git for configuration files for deploying django on to production server

Steps to automate configuration management using Ansible:

step01: Create a virtual machine (remote/guest) and grab the ip address.
        
step02: Install ansible in host machine:

        $ sudo apt update
        $ sudo apt add-repository ppa:ansible/ansible
        $ sudo apt install ansible -y
   
step03: SSH passwordless authentication between (host and guest machines):

        In host:
        $ ssh-keygen       //keep on pressing ENTER until the command terminates
        $ cd .ssh
        $ cat id_rsa.pub  //copy the key
        
        In guest:
        $ cd .ssh
        $ sudo nano authorized_keys    //paste the master's public key
        save and exit
        
        Validate by connecting slave from master: ssh user@slave_ip_address

step04: Create a Inventory file:

        In host:
        $ cd /etc/ansible/hosts
        add the ip address/hostname/domainname of slave in master
        [test]
        server1 ansible_host=<ip_addr> ansible_user=<guest USER>
        save and exit
        
        validate : $ ansible -m ping server1            //returns pong
                   $ ansible -m ping all               //returns pong
                   
step05: Create a project directory in host:

        $ mkdir <project_dir>

step06: Create ansible playbook in host:

        $ cd <project_dir>/ansible
        $ sudo nano main.yml
         paste the main.yml content present in the source : https://github.com/akshaykumart/ansible.git
         
step07: Create ansible roles in host:

        $ cd <project_dir>/ansible
        $ sudo ansible-galaxy init <role_name> 
        $ sudo nano /role_name/tasks/main.yml
          paste the tasks content present in the source : https://github.com/akshaykumart/ansible.git
          save and exit
        $ sudo nano /role_name/handlers/main.yml
          paste the handlers content present in the source : https://github.com/akshaykumart/ansible.git
          save and exit
          NOTE: Modify database name,user,password according to your db deatils
          save and exit

step08: create a vault to store database details:

        $ ansibe-vault create vault.yml
          set the password for vault file
          paste the handlers content present in the source : https://github.com/akshaykumart/ansible.git
          save and exit
        
        $ sudo nano vault_pass.yml
          paste your vault password 
          save and exit

step09: Run the playbook:

        $ cd <project_dir>/ansible
        $ ansible-playbook /etc/ansible/hosts main.yml --vault-password-file vault_pass.yml
          
       
step10: Validate everything in slave machine


        
      
        

        
        

