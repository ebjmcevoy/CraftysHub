# CraftysHub
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(images/Elk_Network.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml files may be used to install only certain pieces of it, such as Filebeat.

  - /filebeat.yml
  - /metricbeat.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting  access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system metrics.

The configuration details of each machine may be found below.

| Name     | Function              | IP Address | Operating System |
|----------|-----------------------|------------|------------------|
| Jump Box | Gateway               | 10.0.0.1   | Linux            |
|  Web 1   | Server (redundancy)   | 10.0.0.2   | Linux            |
|  Web 2   | Server (redundancy)   | 10.0.0.3   | Linux            |
|  Web 3   | Server (redundancy)   | 10.0.0.4   | Linux            |
|  
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the load balancer can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _White listed IP = host machine's IP

Machines within the network can only be accessed by the JumpBox / IP 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses        |
|----------|---------------------|-----------------------------|
| Jump Box |        No           | 10.0.0.5 10.0.0.6 10.0.0.7  |
|          |                     |                             |
|          |                     |                             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it can be applied to multiple machines at once, without the chance of type errors for each individual installation.

The playbook implements the following tasks:
- install docker
- allows access to more memory
- downloads and launches an Elk Container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(images/elk_up.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.6
- 10.0.0.7

We have installed the following Beats on these machines:
- filebeat
- metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is a small log shipper that can collect user specifified logs or events, metricbeat is the same for metrics and statistics.  Either can be prepared to send their information to a centralized area, such as the elk stack.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk, filebeat, and metricbeat .yml files to /etc/ansible.
- Update the /etc/ansible/hosts file to include the three webservers IP under [webserver] and the elk host IP under [elk]
- verify that that host config and the host section of the yml files match, and execute ansible-playbook (chosen yml)

- access http://[your.VM.IP]:5601/app/kibana to test that it is up and running correctly.
