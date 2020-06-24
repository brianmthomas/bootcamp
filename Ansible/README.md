## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![DVWA Network Diagram](Images/DVWA Network Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.



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
- Load balancers protect the Availability aspect of security.
- A "jump box" is a single login point for administrative activities and nothing else, limiting exposure from such non-administrative activities as mail and web browsing.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the application and system configuration.
- **Filebeat** watches for log output
- **Metricbeat** records system performance metrics

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| JumpBox-Provisioner | Gateway  | 10.0.0.4   | Linux            |
| ElkServer     | ElasticSearch engine | 10.0.0.9 | Linux |
| DVWA-VM1 | Application Server | 10.0.0.5 |  Linux |
| DVWA-VM2 | Application Server | 10.0.0.8 |  Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the JumpBox-Provisioner and ElkServer machines can accept connections from the Internet. Access to these machines is only allowed from the following IP address:
- 99.27.123.17

Machines within the network can only be accessed by JumpBox-Provisioner and ElkServer.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes             | 99.27.123.17    |
| ElkServer | Yes             | 99.27.123.17    |
| DVWA-VM1 | No      | 10.0.0.4, 10.0.0.9 |
| DVWA-VM2 | No      | 10.0.0.4, 10.0.0.9 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it saves time and provides repeatable consistency.

The playbook implements the following tasks:
- Uninstall Apache 2 (if present) using **apt**
- Install docker.io using **apt**
- Install python-pip using **apt**
- Install docker using **pip**
- Download DVWA image and start app using **docker_container**

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5
- 10.0.0.9
We have installed the following Beats on these machines:
- Filebeat

These Beats allow us to collect the following information from each machine:
- **Filebeat** forwards syslog entries to ElasticSearch

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the filebeat-configuration.yml file to files/filebeat.yml.
- Update the playbook file to include the address of the ElkServer.
- Run the playbook, and navigate to 10.0.0.9 to check that the installation worked as expected.
