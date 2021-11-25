# Project1
ELK-STACK-PROJECT 
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Diagram for Project1 drawio](https://user-images.githubusercontent.com/89238085/143392288-17714400-140c-442f-8137-955a187af339.png)


These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

https://github.com/PMehtaJ/Project1/blob/main/Ansible%20Playbook

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting _____ to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
With Load balancer you are able provide high availability for the webservers that we created. It covers the Availability aspect from the CIA triad. The Jump box acts as a gateway for the webservers, and it prevents from exposing them to public directly. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the _____ and system _____.
- _TODO: What does Filebeat watch for?_
Filebeat is a light wight installation that collects logs for the ELK stack monitoring. You can specify the location for logs to be collected. You can collect log events and forward them to Elastic serch for it to be searchable and reportable. For this project we are collecting logs from the Web1, Web2 and Web3 to be pushed into Elk Satck 
- _TODO: What does Metricbeat record?_
Metricbeat record collects the metrics and statistics for the server and ships it to the ELK stack for it to be monitored and be searchable. For the project we are able to monitor, the CPU usage, Memory usage and Disk usage for Web1,Web2 and Web3
The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

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
Which machine did you allow to access your ELK VM? What was its IP address?_
Elk Server can only be accessed by my IP address. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
| Jump Box | yes  | 203.220.148.147|
| Web1     |      no    |     10.0.0.7 |
| Web2     |      no     |      10.0.0.7|       
| Web3    |   no       |    10.0.0.7|
| Elk-Server    |   Yes       |    203.220.148.147|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
Ansible is an open source tool that helps automate provisioning of the computing infrastructure and configuring it. The deployment is very simple and the playbooks and the configuration files can be written in YML which make it very easy to read the files compared to other formats

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- Created a Server for the Elk Deployment on Azure
- Added the VM to the existing Ansible configuration file under [Elk]
- Create and Edit Elk.yml to install the required modules for Elk
- Run the ansible playbook  

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

C:\Users\AusBorn PC\Desktop\Project1_ELK_STACK\images)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web1 : 10.0.0.16
- Web2 : 10.0.0.17
- Web3 : 10.0.0.18

We have installed the following Beats on these machines:
- We have installed filebeat and Metricbeat on the Webservers

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc.: 
Filebeat helps you collect centralised data from the devices and is typically used for log management, example syslog . Whereas the metric beat is specific system metric like the CPU, memory that can be used to monitor and alerting in the ELK stack. 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
Ansible playbooks that are configured for 
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
