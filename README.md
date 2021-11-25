# Project1
ELK-STACK-PROJECT 
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram for Project1 drawio](https://user-images.githubusercontent.com/89238085/143392288-17714400-140c-442f-8137-955a187af339.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the configuration file may be used to install only certain pieces of it, such as Filebeat.

[Ansible Playbook](https://github.com/PMehtaJ/Project1/blame/main/Ansible%20Playbook)
[Hosts file](https://github.com/PMehtaJ/Project1/blob/main/Hosts%20File)
[ELK playbook](https://github.com/PMehtaJ/Project1/blob/main/ELK%20playbook)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting unauthorised access to the network.

With Load balancer you are able provide high availability for the webservers that we created. It covers the Availability aspect from the CIA triad. The Jump box acts as a gateway for the webservers, and it prevents from exposing them to public directly. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the netwrok and system logs.

Filebeat is a light wight installation that collects logs for the ELK stack monitoring. You can specify the location for logs to be collected. You can collect log events and forward them to Elastic serch for it to be searchable and reportable. For this project we are collecting logs from the Web1, Web2 and Web3 to be pushed into Elk Satck 

Metricbeat record collects the metrics and statistics for the server and ships it to the ELK stack for it to be monitored and be searchable. For the project we are able to monitor, the CPU usage, Memory usage and Disk usage for Web1,Web2 and Web3
The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.7   | Linux            |
| Web1     |      WebServer 1    |     10.0.0.16       |     Linux             |
| Web2     |      WebServer 2    |      10.0.0.17      |        Linux          |
| Web3    |   WebServer3       |    10.0.0.18        |   Linux               |
| Elk-Server    |   Elk stack server       |    10.2.0.4        |   Linux               |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
Add whitelisted IP addresses_ White listed IP address is my public IP 203.220.148.147

Machines within the network can only be accessed by JumpBox.

Elk Server can only be accessed by my IP address. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
| Jump Box | yes  | 203.220.148.147|
| Web1     |      no    |     10.0.0.7 |
| Web2     |      no     |      10.0.0.7|       
| Web3    |   no       |    10.0.0.7|
| Elk-Server    |   Yes       |    203.220.148.147|

### Elk Configuration

Ansible is an open source tool that helps automate provisioning of the computing infrastructure and configuring it. The deployment is very simple and the playbooks and the configuration files can be written in YML which make it very easy to read the files compared to other formats

The playbook implements the following tasks:
- Created a Server for the Elk Deployment on Azure
- Added the VM to the existing Ansible configuration file under [Elk]
- Create and Edit Elk.yml to install the required modules for Elk
- Run the ansible playbook  
- Install Docker.io, Python-pip, Increase Virtual Memory
- Download and Launch ELK Docker Container 
- Ports 5601 and 9200 were made reachable

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![Docker_ps_output](https://user-images.githubusercontent.com/89238085/143396654-61731e40-5fe9-4e04-8e6d-291866cd2c4e.JPG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 : 10.0.0.16
- Web2 : 10.0.0.17
- Web3 : 10.0.0.18

We have installed the following Beats on these machines:
- We have installed filebeat and Metricbeat on the Webservers

These Beats allow us to collect the following information from each machine:
Filebeat helps you collect centralised data from the devices and is typically used for log management, example syslog . Whereas the metric beat is specific system metric like the CPU, memory that can be used to monitor and alerting in the ELK stack. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the jumpbox and follow the steps below
- Start the Ansible container.
- SSH into the Ansible container
- Copy the filebeat-configuration.yml file to /etc/filebeat/filebeat.yml & Copy the metricbeat-configuration.yml file to /etc/ansible/files
- Update the  file to include the following
     - output.elasticsearch:
       hosts: ["10.2.0.4:9200"]
       username: "elastic"
       password: "changeme"
       --------------------->
       setup.kibana:
       host: "10.2.0.4:5601"

- Run the playbook, and navigate to systemlogs click on check data on the Kibana page to check that the installation worked as expected.
![image](https://user-images.githubusercontent.com/89238085/143398430-69d2f8c4-fdf3-4f77-ac84-ec3e92f27aaa.png)

Filebeat_playbook and Metricbeat_playbook are playbooks and you copy them to etc/ensible folder

Ansible playbooks that are configured for 
You update hosts file to define where the Ansible playbooks will run the elk server to the list. You will need to update the filebeat.yml file to run the ansible playbook 

You can check if your ELK server is running by accessing it on: Piblic IP:5601/app/kibana

Commads that the user will need to run to Elk server are as follows: 
$ssh User@JumpBoxIP
$sudo docker container list -a
$sudo docker start container_name
$sudo docker attach container_name
$cd etc/ansible
$ansible-playbook elk.yml
$ansible-playbook filebeat-playbook.yml
