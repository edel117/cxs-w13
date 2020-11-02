# cxs-w13

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

Images/VirtualNet_diagram.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the pentest.yml file may be used to install only certain pieces of it, such as Filebeat.

  - pentest.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting HTTP traffic to the network.
- Load balancers help keep the connected servers available in case of a large amount of traffic. A Jumpbox acts like a gateway in that it will be the only point to access the virtual network thus increasing security. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the server and system logs.
- Filebeat collects all of the system logs and any other logs that are specified and sent to either logstash and/or elasticsearch (depending on how it was configured).
- Metric beat collects information about the system and from any running services, sending them to either elasticsearch and/or logstash

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name           | Function        | IP Address | Operating System |
|----------------|-----------------|------------|------------------|
| Jump Box       | Gateway         | 10.0.0.1   | Linux            |
| Webserver1     | Hosts dvwa      | 10.0.0.7   | Linux            |
| Webserver2     | Hosts dvwa      | 10.0.0.9   | Linux            |
| Webserver3     | Hosts dvwa      | 10.0.0.10  | Linux            |
| ELK Server     | Hosts ELK Stack | 10.2.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 108.14.4.174

Machines within the network can only be accessed by the JumpBox, webservers, and ELK Server.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address? The ELK VM can be accessed by the JumpBox.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 108.14.4.174         |
| Webserver1 | No                  | 10.0.0.4             |
| Webserver2 | No                  | 10.0.0.4             |
| Webserver3 | No                  | 10.0.0.4             |
| Elk VM     | No                  | 10.0.0.4, 10.0.0.7, 10.0.0.9, 10.0.0.10|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- ...  it is simple to create the yaml file and using a single command to automate the process. The same is true when trying to update the ELK machine.

The playbook implements the following tasks:
- Increase the amount of VRAM
- Install docker.io
- Install python3
- Install docker python module
- Download and Install ELK docker container


The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

Images/ELKContainerRunning.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.7
- 10.0.0.9
- 10.0.0.10
 
We have installed the following Beats on these machines:
- Filebeat
- Metricbeat


These Beats allow us to collect the following information from each machine:
- Filebeat collects all of the system logs and send them all to elasticsearch and Kibana. Metricbeat collects information about the hardware of the machines and sends it to elasticsearch and Kibana.

### Using the Playbook
In order to use the playbooks, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy all the files in the Ansible directory to your /etc/ansible directory in your container. The ansible Ansible directory contains the yaml file for the DVWA container, the yaml file for the ELK container, the yaml files for the filebeat and metricbeat installations. The Ansible directory also contains the necessary configuration files for all containers. 
- Modify the hosts file, that’s included in the Ansible directory, to include private IP addresses in your network.
- Once the pentest.yml and install-elk.yml playbooks have been run, you’ll need to run the filebeat-config.yml and metricbeat-config.yml that are in the files directory. These yml files install filebeat and metricbeat on the DVWA container machines.

- To run the ansible playbooks run the following commands:
-	ansible-playbook install-elk.yml
-	ansible-playbook filebeat-config.yml
-	ansible-playbook metricbeat-config.yml
