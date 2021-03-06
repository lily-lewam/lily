
# lily
Cybersecurity Project 1 

                       Automated ELK Stack Deployment
    
    
    
<img width="916" alt="Screen Shot 2021-05-01 at 1 02 09 PM" src="https://user-images.githubusercontent.com/79333560/116793813-eab07980-aa7d-11eb-9f70-9ecc0177eaa6.png">
  Automated ELK Stack Deployment
       
       



These files have been tested and used to generate a live ELK deployment on Azure.They can be used to either recreate the entire deployment pictured above. Alternatively, a select portion of the playbook file may be used to install only certain pieces of it ,such as filebeat. 
  
   

  
<img width="735" alt="Screen Shot 2021-05-01 at 6 41 27 PM" src="https://user-images.githubusercontent.com/79333560/116799286-de8fe080-aaac-11eb-8c5b-41158461a41d.png">

   
    This documents contains the following details :
Description of the Topology
Access Policies
ELK Configuration
Beats in use
Machines Being Monitored
How to use the Ansible build 
 
 Description of the Topology

 The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application .

Load balancing ensures that the application will be highly reliable, in addition to restricting access to the network .
   What aspects of security do load balancers protect? What is the advantage of a jump box?
       Load balancers protect  the system from DDoS attacks by shifting attack traffic. The advantage of a jump box is to give access to the user from a single node that can be secured and monitored.
     
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system performance with use of filebart and metricbeat . 
    Metricbeat is a lightweight shipper that you can install on your servers to periodically collect metrics from the operating system and from services running on the server. 
Metricbeat Takes the metrics and statistics that it collects and ships them to the output that you specify, such as Elasticsearch or Logstash.

                   The configuration details of each machine may be found below.                                                             
                     +----------+----------+------------+-------------------+
                     | Name     | Function | IP Address | Operating System  |
                     +----------+----------+------------+-------------------+
                     | Jump box | Gateway  | 10.0.0.4   | Linux             |
                     +----------+----------+------------+-------------------+
                     | VM 1     | VM       | 10.0.0.9   | Linux             |
                     +----------+----------+------------+-------------------+
                     | VM 2     | VM       | 10.0.0.8   | Linux             |
                     +----------+----------+------------+-------------------+
                     | VM 3     | VM       | 10.0.0.5   | Linux             |
                     +----------+----------+------------+-------------------+
                     | ELK      | ELKstack | 10.2.0.4   | Linux             |
                     +----------+----------+------------+-------------------+



     
Access Policies
The machines on the internal network are not exposed to the public Internet.
 
Only the Jump Box machine is only allowed from the following IP addresses:
 104.41.143.57 

Machines within the network can only be accessed by port 22.
     

Which machine did you allow to access your ELK VM? What was its IP address? 
  Jump box ip 10.0.0.4
 
A summary of the access policies in place can be found in the table below.

 | Name     | Publicly Accessible  | Allowed IP Addresses |   |
|----------|----------------------|----------------------|---|
| Jump Box | yes/no               | 10.0.0.4             |   |
| VMs      |  no                  | 10.0.0.4             |   |
| ELK      |  no                  | 10.0.0.4             |   |


ELK Configuration 

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually , which is advantageous because it can be run from the command line through multiple computers and ensure the scripts remain the same everywhere .

What is the main advantage of automating configuration with Ansible?
It is very simple to set up and used for creating the playbooks in YAML.

     The playbook implements the following tasks:
     Increasing the memory of the machine 
     Create a yml file
     Install Docker.io
     Install Python3
     Install docker
     Install the elk container and run ansible-playbook install-elk.yml

                 Image install-elk.yml
                 
<img width="827" alt="Screen Shot 2021-05-01 at 7 50 52 PM" src="https://user-images.githubusercontent.com/79333560/116800593-74306d80-aab7-11eb-81cf-7e1465a5cfa7.png">
                 







<img width="1198" alt="Screen Shot 2021-05-01 at 7 02 43 PM" src="https://user-images.githubusercontent.com/79333560/116799763-2401dd00-aab0-11eb-9371-fff632423c68.png">








 
 

Target Machines and Beats

This ELK server is configured to monitor the following machines:
 - WEB 1: 10.0.0.9
 - WEB 2: 10.0.0.8
 - WEB 3: 10.0.0.5 

We have installed the following Beats on these machines:
Filebeats and Metricbeats were installed .

                     Filebeats collects and forwards data from the file system and sends the information to the ELK stack server for processing. We can view the information through kibana charts and tables.
         Metricbeats takes the metrics and statistics that collects from operating system and ships them to the output that you specify ,such as Elasticsearch or logstach.

             Using the playbook 
 In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have sudh a control node provisioned.

 SSH into the controle node and follow the steps below:
Copy the playbook.yml file to roles.
Update the config.yml file to include..
Run the playbook, and navigate to kibana to check the installation worked as expected.

              Answer the following question to fill in the blanks :
           
Which file is the playbook? Where do you copy it? 
    . FileBeat and MetricBeat
    . Copy under /etc/ansible/roles 

Which file do you update to make Ansible run the playbook on a specific machine? The Host file

How do i specify which machine  to install the ELK server on versus which to install filebeat on ?
    The Host file allows under webservers Web 1,2 and 3 create under the same web servers.
   And create for ELK a separate under elk .
   
           [webservers]
           
      10.0.0.9 ansible_python_interpreter=/usr/bin/python3
      
      10.0.0.8 ansible_python_interpreter=/usr/bin/python3
      
      10.0.0.5 ansible_python_interpreter=/usr/bin/python3

            [elk]
        10.2.0.4 ansible_python_interpreter=/usr/bin/python3

   
Which URL do you navigate to in order to check that the ELK server is running? 
  http:// my VM ip :5601/app/kibana

     Bonus, provide the specific commands the user will need to run to download the playbook, update the files, etc

            /etc/ansible/roles ansible-playbook filebeat-playbook.yml
           
            /etc/ansible/ ansible-playbook install-elk.yml
            
           /etc/ansible/files  ansible-playbook filebeatconfig.yml
           
           /etc/ansible ansible-playbook my-playbook
           
           /etc/ansible ansible-playbook ansible.cfg
           
                  
                  
       - Command to connect Jump-Box is ssh azadmin@104.41.143.57 ( username@VM-Public-IP)
       - once you are conncetd check sudo permission ( RUN sudo-l ) sudo permission without requiring a password .

              To configure your jump box to run Docker containers and to install a container.
              
            - TO install docker.io on your Jump box 
                RUN:- sudo apt update
                THEN RUN :- sudo apt install docker.io
            - Verify that the Docker service is running
                sudo systemctl status docker
                
            Once Docker is installed, pull the container cyberxsecurity/ansible
               Run sudo docker pull cyberxsecurity/ansible
               Run sudo su to switch to root 
               Run docker run -ti cyberxsecurity/ansible:latest bash to start the container
               Run exit to quit .
               
             - To see the name of your container RUN command sudo (docker container list -a)
             - To Check for your Ansible container command (sudo docker ps)
             - To to start container RUN command (sudo start name of your conatiner) 
             - To Connect the Ansible container (sudo attach container name )
             - To change to ansible directory RUN (cd /etc/ansible)
             
             - To connect to ELK ssh azadmin@10.2.0.4 (RUN username@ELK-private-ip)
  
                
              
        
      
                

