ANSIBLE LAB PRACTISE :: Khaja Sir class Room Notes:
Date: 20-02-2023
Explained: CI/CD pile and Ansible role as part of pipelines its feature
>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
Date: 21-02-2023
	Take 2 servers from azure/Aws for Practice with ports all enabled & connect though Password
	Check the Communication access: ping from both
	Install ansible on one node
	Cd /tmp
	Vi host > add the other node
	ansible -i hosts -m ping all
	
	Write an playbook and lets check the things
---
- name: hello
  hosts: all
  become: yes
  tasks:
    - name: install tree
      package:
        name: tree
        state: present

Date: 21-02-2023
	Take 2 servers from azure/Aws for Practice with ports all enabled & connect though Password
	ssh username@ipadd/hostname   (or)  ssh -i  <path to pem> username/ip
once connect the VM we will do the following steps:
>> Ansible Control Node
>> Node
Sftp -I ansible.pem ubuntu@<Public ip>
Put 
Bye>
Connect to Ansible Control node
	Python3 –version
	Install Ansible on Control Node 
	Ansible –version
	ls -sl
	chmood 400 ansible.pem
vi hosts:
 >>  Add the Private ip  >> (Node-1 Ip need to Mentioned)
ansible -i hosts -m ping all
>> cant connect due to no Passwd/SSH key:
	ansible –help
	ansible --private-key ansible.pem -i hosts -m ping all
	we need to create the common user for to connect the all servers (Username = Devops)
	
sudo vi /etc/ssh/sshd_config  or sudo nano /etc/ssh/sshd_config
sudo service sshd restart              >> we have do in Ansible Control Panel server same in Node Server
AND
sudo vi /etc/ssh/sshd_config  or sudo nano /etc/ssh/sshd_config
sudo service sshd restart              >> we have do in same in Node Server

sudo adduser devops  (or) sudo useradd devops
P/W: devops
Cat /etc/passwd >> >> we have do in control Panel server same in Node Server

sudo adduser devops  or sudo useradd devops
P/W: devops
Cat /etc/passwd >> >> we have do in same in Node Server

Example:
Sudo visudo
Devops ALL=(ALL:ALL) ALL
Su devops
P/W:
Sudo apt update
devops ALL=(ALL:ALL) NOPASSWD:ALL
su devops
cd ~
sudo apt update

>> Same do for Node 2 Server As well
Example:
Sudo visudo
Devops ALL=(ALL:ALL) ALL
Su devops
P/W:
Sudo apt update
devops ALL=(ALL:ALL) NOPASSWD:ALL
su devops
cd ~
sudo apt update

##Copy the Public key into Node Serversudo 
>> Now Connect in Ansible Node Do the Work for below Actions
sud devops
whoami
create a keypair
>ssh-keygen
Ls -al ~/.ssh/
Cat ~/.ssh/id_rsa.pub
Cat ~/.ssh/id_rsa
To copy the content we are using 
ssh-copy-id devops@Private-IPof <node server  -- devopsss>
if we want to login the Node Server we simply do it
	Ssh -I ~/.ssh/id_rsa devops@<Private-IP>
Ssh devops@<Private IP>
Ssh <PrivateIP> because user name is same of both user

IF you Same do for Node Server Please Check it once
Su devops@<Private IP of Control Node Server>
We need to enter password manually bcz we are not added the ssh connection between node to Ansible control panel:

-------------------
--
Ansible -I hosts -m ping all

Date :: 23-02-2023
Writing Play books   ::  First Playboook
	Start the 2 AWS machines and the do the perform :
	Create the one more machine for manual test practise
Ssh -I ansible.pem ubuntu@IP >> for Test server:
>> cd /
>> ls
>> tree
>> sudo apt update
>> sudo apt install tree
>> Tree 
>> cd ~
>> ls -al
>> mkdir 1 2
>> touch 1/{1..10}.txt
>> touch 2/{11..20}.txt
>> tree
>>>>>
First.yaml

>>>>>>>>>>>	
			---
- name: install tree			
hosts: all			
become: yes			
tasks:			
- name: install tree on ubuntu			
ansible.builtin.apt:			
name: tree			
update_cache: yes			
state: present			

>>>>>>>>>>>
Control Node:
Mkdir first
Cd first/
Vi first.yaml
>>
>>
Vi hosts
	Add the node 1 IP >Private ip
Su devops
Cd ~
Mkdir playbooks
Cd playbooks
Vi hosts
Vi first.yaml
>>
>>
Ansible-playbook -I hosts first.yaml
>> again loged into node1 IP
Check tree command
Sudo apt purge tree
Again : Excute the same command in Asnsible control Node
Again: Above step for any logs changed or not:
----
** Modules**
Sudo apt update
Sudo apt install nginx
Sudo systemctl status nginx.service
From Ansible we need to do
Activty1 > hosts
Hosts>
Node 1 > IP added
nginx.yaml
>>>
Write a playbook
>>>
Excute In ansible control node
ssh devops@PublicIP
>>
Ls
Cd playbooks/
Mkdir actvity1
Cd activty1
Vi hosts
Vi nginx.yaml
<copy and wirte the Playbook>
-
Check Syntax Check:
ansible-playbook – help
ansible-playbook -I hosts – syntax-check nginx.yaml
write and done some Changes for Yaml Syantax:
ansible-playbook -I hosts – syntax-check nginx.yaml
write and done some Changes for Yaml Syantax:
	Lets execute dry run ( does not work in all casess)
>>>> Ansible-playbook – help
>>>> Ansible-playbook -I hots -- check nginx.yaml
>>> ansible-playbook -I hosts nginx.yaml
Connect Node1: Check with Post Nginx Working or Not
>>> again Do once again: ansible-playbook -I hosts nginx.yaml
Check the results:
Ansible-playbook -I hots – check nginx.yaml
Activity 2: Install Apache:
In test Machine:
# ubunu
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2

# redhat steps
sudo dnf install httpd
sudo systemctl enable httpd.service
sudo systemctl start httpd.service
-
Sudo apt purge apache2 
Sudo apt purge nginx
>>
In assible control Node
ansible -i hosts -m ansible.builtin.apt -a “name=nginx purge=yes state=absent” -b all
ansible -i hosts -m ansible.builtin.apt -a “name=nginx purge=yes state=absent” -b all
browse the 2nd Node:
ansible -i hosts -m ansible.builtin.apt -a “name=nginx purge=yes state=absent” all
ansible-playbook -i hosts –- check nginx.yaml
sudo systemctl status 
sudo apt purge nginx.service
sudo apt auto remove
sudo apt purge nginx.service
sudo apt – help
>
Browse the Node1IP > it is Not Working
->
We need to do the manual step while start as well form Deletion as well.
>>in test server as well
Sudo apt autoremove
<<>>>>
 
 ------------------------>>>>>>------------------------>>>>>>---------------
Date:: 24-02-2023:
Ansible Modules:
*) Need to Allow ports at NSG Levels in azuere/AWS for Nginx port acces
---->
sudo apt update
sudo apt install nginx -y
sudo systemctl status nginx.service
Browse the Pasge>>
>>
Write YAMl File
Ansible-playbook –help
ansible-playbook -i hosts -- syantax-check nginx.yaml
Prove a Point :: do some Changes in yaml for above command Working.NOT
>>
DRY Run Execution Uses:: Not 100% Good
ansible-playbook -i hosts -- check nginx.yaml
Ansible-playbook -i hosts nginx.yaml
Again:
Ansible-playbook -i hosts nginx.yaml
Ansible-playbook -i hosts –- check nginx.yaml

>>>>>  In test Machinne: 
Installing apache on Ubuntu
# ubunu
sudo apt update
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
Browse the Test Machine:>>
We need to uninstall nginx because Nginx & Apcahe on same port 
Sudo apt purge nginx
Sudo 
>> Ansible adhoc Comands in google
>>>>>
Apt module in ansible for nginx uninstall:
ansible -i hosts -m ansible.builtin.apt apt -a "name=nginx purge=yes state=absent" -b all
Again:
ansible -i hosts -m ansible.builtin.apt apt -a "name=nginx purge=yes state=absent" -b all
>>
Connect: Ssh <Node1-IP>
Check Nginx is Running pr Not..?
ansible -i hosts -m ansible.builtin.apt apt -a "name=nginx purge=yes state=absent" -b all

sudo apt purge nginx
sudo apt autoremove nginx
sudo systemctl status mginx.service
sudp apt – help
Now Browse the Node IP:
--
*********Important Node:*******
We need to know manual steps: From end to end like Install & Uninstall we need to know
AdHoc Command for Example:
ansible -m ansible.builtin.apt -a “name=nginx update_cache=yes State=present” -i hosts
In test Server wehave installed Apche
Sudo apt autoremove

AS of now Important commands
ansible-playbook -i hosts --syntax-check nginx.yaml
ansible-playbook -i hosts --check nginx.yaml
ansible-playbook -i hosts nginx.yaml
Sudo apt autoremove
sudo apt purge nginx
sudo systemctl status nginx.service
-------------------------
###Instaling apache on redhat8 ####
Activity:
Redhat
Ubuntu
Apache.yaml

##
Systemctl in ansible

Apply on Test Machine
>>
Create one more VM for : Redhat
# redhat steps
sudo dnf install httpd
sudo systemctl enable httpd.service
sudo systemctl start httpd.service
sudo systemctl status httpd
sudo systemctl enable httpd
sudo systemctl start httpd
>>
Create node2 for redhat instance:
Python –- version
Password authentication 
Yes 
Yes – mentioned in 2 places
Sudo systemctl restart sshd
Sudo adduser devops
Sudo passwd devops
Need to give Admin permission
Sudo vissudo
>>
Sudo systemctl restart service
Ssh devops@
-
Node 3:
------------->>>>------>>>>>--------------------

Date:: 25-02-20023
Ansible -m ansible.builtin.setup -I hosts ubuntu
	Ansible -m ansible.builtin.setup -I hosts ubuntu > ~/facts.json
	Sftp devops@IP
	get facts.json
	bye

Ansible -m ansible.builtin.setup -i hosts redhat
Ansible -m ansible.builtin.setup -a “filter=distribution” -i hosts all
Ansible -m ansible.builtin.setup -a “filter=*family*” -i hosts all
>> Write an Yaml file for Apche intsall on ubuntu & reshat with conditions mentioned.
Ansible-playbook -i hosts –syntax-check apache.yaml
Ansible-playbook -i hosts apache.yaml
>> write An Yaml file and changes the variable and lets check the output
Ex: 
>package_name=httpd 
> "{{ package_name }}"
Ansible-playbook -i hosts –syntax-check apache.yaml
Ansible-playbook -i hosts apache.yaml
4 steps converted into 2 steps (Duplicate, additional,)
>> write An Yaml file and Bailout Method lets check the output

Date: 27-02-2023

ansible.builtin.fail:
        msg: "This playbook is designed only for RedHat and Debain os families"
      when: ansible_facts['os_family'] != 'RedHat' and ansible_facts['os_family'] != 'Debian'
#when: ansible_facts['os_family'] == 'RedHat' or ansible_facts['os_family'] == 'Debian' >> excute 1st then check the above statement




