## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

UNCC-CyberSecurity\Diagrams\Casey Johnson_Week_13_PROJECT_ELK1.png

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - UNCC-CyberSecurity\Ansible\install-elk.yml

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
- Load balancers protect application availability, allowing client requests to be shared across a number of servers
  The advantage of a Jump Box is that it minimizes the attack surface by ensuring remote connections to the cloud network come through a single VM. Additionally, remote connections to the Jump Box can be monitored easily to identify unusual remote connections.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.
- Filebeat is used to monitor log files
- Metricbeat is used to collect operating system and service statistics from monitored VM's

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| WEB-1    | DVWA     | 10.0.0.7   | Linux            |
| WEB-2    | DVWA     | 10.0.0.9   | Linux            |
| WEB-3    | DVWA     | 10.0.0.12  | Linux            |
| ELK-1    | ELK      | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 172.58.236.242

Machines within the network can only be accessed by the Jump Box.
- The Jump Box can access the ELK VM Elk-1 using SSH. The Jump Box's IP address is 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
|Jump Box  |	Yes (SSH)	 | 172.58.236.242	|
|Web-1     |    Yes (HTTP)	 | 172.58.236.242	|
|Web-2	|	Yes (HTTP)	 | 172.58.236.242       |
|Web-3	   |	Yes (HTTP)	 | 172.58.236.242       |
|Elk-1	   |    Yes (HTTP)	 | 172.58.236.242       |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Build and deployment is performed automatically, consistently and quickly
  Consistent, rapid configuration and deployment of virtual machines ensure all prescribed security measures can be scripted to minimize attack surfaces while enabling horizontal and elastic scaling by deployment to more or fewer virtual machines in a cluster as required to meet capacity demand.
  Facilitates OS and software updates

### Playbooks:

The playbook implements the following tasks:
- Playbook 1: pentest.yml
  pentest.yml is used to set up DMWA servers running in a Docker container on each of the web servies show in the diagram above. It implements the following tasks:

  Installs Docker
  Installs Python
  Installs Docker's Python Module
  Downloads and launches the DVWA Docker container
  Enables the Docker service
  Playbook 2: install-elk.yml
  install-elk.yml is used to set up and launch the ELK repository server in a Docker Container on the ELK server. It implements the following tasks:

  Installs Docker
  Installs Python
  Installs Docker's Python Module
  Increase virtual memory to support the ELK stack
  Increase memory to support the ELK stack
  Download and launch the Docker ELK container
  Playbook 3: filebeat-playbook.yml
  filebeat-playbook.yml is used to deploy Filebeat on each of the web servers so they can be monitored centrally using ELK services running on Elk-1. It implements the following tasks:

  Downloads and installs Filebeat
  Enables and congigures the system module
  Configures and launches Filebeat

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- WEB-1: 10.0.0.7
  WEB-2: 10.0.0.9
  WEB-3: 10.0.0.12

We have installed the following Beats on these machines:
- Filebeat
  Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat collects and ships (sends to ELK for collation, persistence and reporting) logs from VMs running the Filebeat agent
Metricbeat collects and ships system metrics from the operating system and services of VMs running the Metricbeat

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook file to Ansible Docker Container.
- Update the Ansible Host file /etc/ansible/hosts/ to include the following: 
[webservers]
10.0.0.7 ansible_python_interpreter=/usr/bin/python3
10.0.0.9 ansible_python_interpreter=/usr/bin/python3
10.0.0.12 ansible_python_interpreter=/usr/bin/python3

[elk]
10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to Web-1/2/3 or Elk-1 (ssh azadmin@10.0.0.7, ssh azadmin@10.0.0.9 , ssh azadmin@10.0.0.12) to check that the installation worked as expected.
