# Vian_Cyber_Projects
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

/etc/ansible/filebeat-config.yml
/etc/ansible/filebeat-playbook.yml
/etc/ansible/metricbeat-config.yml
/etc/ansible/metricbeat-playbook.yml
/etc/ansible/elkplaybook.yml
/etc/ansible/pentest.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting traffic to the network.
What aspect of security do load balancers protect? Protects against unauthorized/unwanted traffic such as DDoS attacks
What is the advantage of a jump box? It adds security to web servers through rules within the network security group which prevents the servers from being exposed or exploited.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
What does Filebeat watch for? Monitors log data and collects log events
What does Metricbeat record? Records metrics from the system and services running on the server

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name      | Function | IP Address | Operating System |
|-----------|----------|------------|------------------|
| Jump Box  | Gateway  | 10.0.0.4   | Linux            |
| Web 1     | VM       | 10.0.0.8   | Linux            |
| Web 2     | VM       | 10.0.0.9   | Linux            |
| Elk       | Host     | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses: My Public IP

Machines within the network can only be accessed by Jump Box 20.248.194.0

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | My personal IP       |
| Web 1    | No                  | 10.0.0.4             |
| Web 2    | No                  | 10.0.0.4             |
| Elk      | Yes                 | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time and is flexible to change processes/tasks within the VMs it is attached to

The playbook implements the following tasks:

Install docker.io
Install pip3
Install Docker python module
Increase virtual memory
Download and launch a docker
Enable service docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
>![TODO: Update the path with the name of your screenshot of docker ps output]
>![Alt text](http:///Users/Nick/Documents/docker_ps_output.png )


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name      | Function                         | IP Address | Operating System |
|-----------|----------------------------------|------------|------------------|
| Web 1     | Host for container running DVWA  | 10.0.0.8   | Linux            |
| Web 2     | Host for container running DVWA  | 10.0.0.9   | Linux            |

We have installed the following Beats on these machines:
filebeat and metricbeat

These Beats allow us to collect the following information from each machine:
filebeat collects log data/events on the server such as unsuccessful logon attempts.
metricbeat collects system metrics for the servers/machines it is attached to such as memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible.cfg file to /etc/ansible/
- Update the hosts file to include Web 1, Web 2 and elk
- Run the playbook, and navigate to http://13.70.153.96:5601/app/kibana#/home to check that the installation worked as expected.

Answer the following questions to fill in the blanks:
- Which file is the playbook? filebeat-playbook.yml
- Where do you copy it? /etc/ansible/
- Which file do you update to make Ansible run the playbook on a specific machine? hosts
- How do I specify which machine to install the ELK server on versus which to install Filebeat on? Created a separate [elk] group with the private IP address where the VM is located under the [webservers] where filebeat is installed under the IPs and VMs of Web 1 and Web 2 
- Which URL do you navigate to in order to check that the ELK server is running? (elk server IP through port 5601) http://13.70.153.96:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
