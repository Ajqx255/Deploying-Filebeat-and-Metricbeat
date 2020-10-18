# Deploying-Filebeat-and-Metricbeat
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Images/Network pt.1 & Images/Network pt.2]

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  - Playbook-Files/filebeat-playbook.yml & Playbook Files/metricbeat-playbook.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.
 
Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the System Log Files and system Performance.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| Web-3    | Server   | 10.0.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Load Balancer machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: My Public IP 

Machines within the network can only be accessed by the Ansible Container inside the Jumpbox Machine.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | No                  | 10.0.0.4 10.0.0.5    |
| Absible  | No                  | 10.0.0.6 10.0.0.7    |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it was created and configured Infrastuctor as Code, so it can be duplicated, shared, and re created easily

The playbook implements the following tasks:
- Install docker.io
- Install python-pip3
- Install docker module
- Increase memory
- Download and launch docker ELK

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1
- Web-2
- Web-3

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to colloct data on file logs and any changes that might have taken effect throuh malicious means or not. Where as metricbeat checks how the hardware performance is doing and if there is any abnormalities like a huge spike in resources. If ther is we can then verify the issue and fix the problem or correct any changes. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-playbook.yml & metricbeat-playbook.yml file to /etc/ansible Inside your ansible container. nano (file name) and paste YAML code
- Update the Playbook file to include your hosts, current version, 
- Run the playbook, and navigate to your server to check that the installation worked as expected.

_Common Questions: 
- _Which file is the playbook? Where do you copy it?_
- There are two playbook files. filebeat-playbook.yml and metricbeat-playbook.yml. They are both located in the playbook-files folder. 
- You would copy the YAML files into your ansible container in /etc/ansible and make a new file with same or different name ending in .yml. 
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- You well update your /etc/ansible/hosts file include the group name ex: [Webservers] and underneath that you will add your server IP ex: web-1 10.0.0.5 ansible_python_interpreter=/usr/bin/python3 <The path should be something that is preinstalled.> Then when you are copying the YAML file you will need to edit which group you want the changes to take effect in. So if you have a [elk] 10.1.0.5 ansible_python_interpreter=/usr/bin/python3 & [Webservers] 10.0.0.5 ansible_python_interpreter=/usr/bin/python3 and in the YAML file under hosts you will choose Webservers or elk. 
- _Which URL do you navigate to in order to check that the ELK server is running?
- You take the public ip of your webserver ex: http://xx.xx.xx.xx:xxxx and see if you can access your server

Here are specific commands you will need to run to download the playbook, update the files, etc._
ansible-playbook (filename) to run the playbook, 
ansible-playbook (filename) --list-hosts,
ansible-playbook (filename) --list-tasks,
ansible-playbook (filename) -C or --check,
ansible-playbook -h,
or go to:
https://github.com/Ajqx255/ELK-Project-/blob/main/Linux/Linux%20Commands.txt
