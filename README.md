# ansible
configuration management using ansible
This page will include the steps to automate the installations of required packages and deploying django application into a remote machine

step01: Create a virtual machine (remote/guest) of your choice and install ansible into it:
        $ sudo apt update
        $ sudo apt add-repository ppa:ansible/ansible
        $ sudo apt install ansible -y
        
step02: Install ansible in host/ master machine:
        $ sudo apt update
        $ sudo apt add-repository ppa:ansible/ansible
        $ sudo apt install ansible -y
   
step03: SSH passwordless authentication between Master and Slave (host and guest machines):
        In master:
        $ ssh-keygen       //keep on pressing ENTER until the command terminates
        $ cd .ssh
        $ cat id_rsa.pub  //copy the key
        
        In slave:
        $ cd .ssh
        $ sudo nano authorized_keys    //paste the master's public key
        save and exit
        
        Validate by connecting slave from master: ssh user@slave_ip_address

step04: Create a Inventory file:
        In master:
        $ cd /etc/ansible/hosts
        add the ip address/hostname/domainname of slave in master
        [test]
        slave1 ansible_host=<ip_addr> ansible_user=<slave USER>
        save and exit
        
        validate : $ ansible -m ping slave1            //returns pong
                   $ ansible -m ping all               //returns pong
                   
step05: Create a project directory in master:
        $ mkdir <project_dir>

step06: Create ansible playbook in master:
        $ cd ansible/<project_dir>
        $ sudo nano main.yml
         paste the main.yml content present in the source : https://github.com/akshaykumart/ansible
step07: Create ansible roles in master:
        $ cd ansible/<project_dir>
        $ sudo ansible-galaxy init <role_name> 
        $ sudo nano /role_name/tasks/main.yml
          paste the tasks content present in the source : https://github.com/akshaykumart/ansible
          save and exit
        $ sudo nano /role_name/handlers/main.yml
          paste the handlers content present in the source : https://github.com/akshaykumart/ansible
          save and exit
        $ sudo nano /role_name/vars/main.yml
          paste the vars content present in the source : https://github.com/akshaykumart/ansible
          save and exit

step08: Run the playbook:
        $ cd ansible/<project_dir>
        $ ansible-playbook /etc/ansible/hosts main.yml
       
step09: Validate everything in slave machine


        
      
        

        
        

