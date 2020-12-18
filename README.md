# Project-1
Networking, Cloud security, and ELK stack infrastructure/deployment
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagrams/Azure Private Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible file may be used to install only certain pieces of it, such as Filebeat.

 

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.



The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| Web1     | WebServer| 10.0.0.5   | Linux            |
| Web2     | WebServer| 10.0.0.6   | Linux            |
| Web3     | WebServer| 10.0.0.7   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
67.180.232.80

Machines within the network can only be accessed by the jump box 10.0.0.4 .


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.4    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is more secure and less margain for human error.


The playbook implements the following tasks:
- The first task in the playbook is to install docker.io on the elk server using the apt module.
- Second task using apt module is to install python3-pip on the elk server.
- The third task is to use the pip module we just installed in the second task and use it to install the docker module to the elk server.
- Fourth task is to use the command module and increase the virtual memory of the elk server so it has enough RAM to run efficently.
- The last task is to use the docker_container module and download and install the actual container to run on the elk server and include the ports that the elk server runs on.

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
10.0.0.5, 10.0.0.6, 10.0.0.7

We have installed the following Beats on these machines:
Filebeat, and Metricbeat

These Beats allow us to collect the following information from each machine:
Filebeat collects logs of any file changes or updates on the system and sends it to the ELK server for example, `Winlogbeat` collects Windows logs, which we use to track user logon events, etc. Metricbeat collects machine metrics such as uptime of the system os.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the ansible_config file to the elk server ansible directory.
- Update the host file to include the new elk server IP 
- Run the playbook, and navigate to http://(elk server public IP):5601/app/kibana to check that the installation worked as expected.
