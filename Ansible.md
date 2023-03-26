prerequisite :

Python on all machine.


Can Ansible control node be installed on a Windows operating system?
Can Ansible run on Windows?  No, Ansible can only manage Windows hosts. Ansible cannot run on a Windows host natively, though it can run under the Windows Subsystem for Linux (WSL).






Creating an instance:
(Master)
1. Navigate to EC2
2. Launch an instance
3. Select a Linux/Ubuntu OS
4. Continue with the Instance with all default settings, Add Tag is needed. (A tag is a label that you or AWS assigns to an AWS resource. Each tag consists of a key and a value. For each resource, each tag key must be unique, and each tag key can have only one value. You can use tags to organize your resources, and cost allocation tags to track your AWS costs on a detailed level.)
5. Create a Key pair (Works like a Username and Password to connect to the AWS Instance i.e. A key pair, consisting of a public key and a private key, is a set of security credentials that you use to prove your identity when connecting to an Amazon EC2 instance. Amazon EC2 stores the public key on your instance, and you store the private key.) (download for future reference)    
  ![image](https://user-images.githubusercontent.com/26665659/227781807-9a55bf85-a5b3-4920-a9cc-ed8ebf5311a7.png)
  ![image](https://user-images.githubusercontent.com/26665659/227782112-7d8aba34-60ff-4fca-bf53-f3b7111bb7c3.png)
  ![image](https://user-images.githubusercontent.com/26665659/227781850-a5c20d55-84b2-42cb-a4d6-dab654ea4064.png)
6. Continue with default security group. 
  ![image](https://user-images.githubusercontent.com/26665659/227782318-73344b4b-f677-4001-bb7d-11c8ba73771f.png)
7. Launch. 
8. Once all setup is done we will have a new instance created. 
  ![image](https://user-images.githubusercontent.com/26665659/227782452-9889d960-6cad-4f1c-a8e2-b2b757267f69.png)
9. fjgh
10. dfjhfhktu
11. hfsdjykd

(Slave / Node)
1. Navigate to EC2
2. Launch an instance
3. Select a Linux/Ubuntu OS
4. Continue with the Instance with all default settings, Add Tag is needed.
5. Add the same Key pair
6. Continue with default security group. 
7. Launch. 
8. Once all setup is done we will have a new instance created. 

Connect to the isntance

(Master)

1. select the EC2 instance and click on connect, under SSH client copy the SSH command
2. ![image](https://user-images.githubusercontent.com/26665659/227782788-6e03638a-066c-49c2-908f-901af6b68a8f.png)
3. Open the Cmd prompt where the Key pair is saved.
4. Paste the copied command in the CMD. and type "yes" to add the local machince to the known host file. Hence, adding your IP to the instance file as a user who can connect and communicate.
5. ![image](https://user-images.githubusercontent.com/26665659/227783433-7a944720-bb49-4de3-a3aa-4eb338d2ea5f.png)
6. The Cmd prompt must have a welcome msg and your local machine will be connected to the Master instance.
7. Become a root user with the following cmd :  "sudo -i" 
8. ![image](https://user-images.githubusercontent.com/26665659/227783760-69897038-b0ea-470c-af94-90bb140e3d83.png)
9. Use the following cmds to configure the PPA on your system and install Ansible run these commands: (please use "exit" cmd to get out of root before running these commands)
10. $ sudo apt update // to update
$ sudo apt install software-properties-common // This software provides an abstraction of the used apt repositories. It allows you to easily manage your distribution and independent software vendor software sources.
$ sudo add-apt-repository --yes --update ppa:ansible/ansible // to create a ansible repo
$ sudo apt install ansible
11. sudo adduser ansible //(the user that will be used for all ansible configurations, as there is no agent on the slave / node instances we have to add user and give them privileges) 
12. ![image](https://user-images.githubusercontent.com/26665659/227793637-d159485c-35bd-4663-b0a4-c7344b44a9b4.png)
13. sudo -i
14. visudo 
15. Add ansible as sudo user 
16. ![image](https://user-images.githubusercontent.com/26665659/227795997-67b05e06-b766-4c68-b6b8-4df9ac0337be.png)
18. vi /etc/ssh/sshd_config (Change "PasswordAuthentication" from No to Yes) (AWS restriction setting)
19. ![image](https://user-images.githubusercontent.com/26665659/227794640-851b28a6-7713-4cd8-992f-ed0efde0565e.png)
20. save and exit, by Prssing ESC then using (":wq") cmd
21. Restart ssh  - "service ssh restart"
22. Now we will use our localhost as a user with cmd - "ssh ansible@localhost"
23. ![image](https://user-images.githubusercontent.com/26665659/227795539-baa8f1d4-8ff3-4150-a7c9-4e96128bf95c.png)  
24. To check the sudo privieleges of "ansible" User use cmd - "sudo apt-get update"
25. Once you complete **Step  1 - Step 24** for connecting localhost to slave 
26. You can now connect your master instace with your slave/node instance with the following cmd - "ssh ansible@<slave / node ip-address>" // we can use public/ private IP as we are connecting using the Master which is in the same Network as they are under the same AWS account, public IP is used to connect from outside the network and Private is used to connect within the network.
27. To check if everything is working right u can "sudo apt-get update" on your slave machine.
28. exit using "exit" cmd
29. Steps to generate the key to establish a direct connect - 
30. $ "su ansible"
31. $ cd ~
32. $ pwd // in user's home directory
33. $ ssh-keygen //SSH KEY GENERATION (private key)
34. ![image](https://user-images.githubusercontent.com/26665659/227803338-ec4d7c5b-d093-4c8c-8b3c-833db88ece51.png)
35. $ ssh-copy-id ansible@<Node/slave Private DNS> //Generate public key on Node/Slave instance
36. $ ssh <Private DNS (i.e. hostname)> // to connect to Node/Slave using hostname
37. 



(Slave / Node Instance)
Open a new cmd prompt for node instance
1. Select the EC2 instance and click on connect, under SSH client copy the SSH command
2. Open the Cmd prompt where the Key pair is saved.
3. Paste the copied command in the CMD. and type "yes" to add the local machince to the known host file. Hence, adding your to the instance file as a user who can connect and communicate.
4. The Cmd prompt must have a welcome msg and your local machine will be connected to the Node instance.
5. Once connected check if python is installed.
6. use cmd - "python3"
7. ![image](https://user-images.githubusercontent.com/26665659/227798129-7a2e82d7-7b39-415b-8dc4-1985fb3953fb.png)
8. Become a root user with the following cmd :  "sudo -i" 
14. visudo 
15. Add ansible as sudo user 
16. ![image](https://user-images.githubusercontent.com/26665659/227801186-d344b187-a5f3-40d1-88a0-4484318e3d42.png)
17. vi /etc/ssh/sshd_config (Change "PasswordAuthentication" from No to Yes) (AWS restriction setting)
18. ![image](https://user-images.githubusercontent.com/26665659/227794640-851b28a6-7713-4cd8-992f-ed0efde0565e.png)
19. save and exit, by Prssing ESC then using (":wq") cmd
20. Restart ssh  - "service ssh restart"
21. Now we will use our localhost as a user with cmd - "ssh ansible@localhost"
22. ![image](https://user-images.githubusercontent.com/26665659/227795539-baa8f1d4-8ff3-4150-a7c9-4e96128bf95c.png)  
23. To check the sudo privieleges of "ansible" User use cmd - "sudo apt-get update"
24. 
25. 

Reference :

1. https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu





