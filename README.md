### ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

elkstack_ts/Diagram/Elk_Stack_project.PNG

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the elkstack_ts/Ansible/filebeatplaybook.yml file may be used to install only certain pieces of it, such as Filebeat.

 

This document contains the following details:
- Description of the Topology
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.e

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway           | 10.0.0.1   | Linux      |
| Elk         |   ElasticSearch    |  10.1.0.4  |   Ubuntu |
| Web 1    |  Web Server        |  10.0.0.5  |  Ubuntu  |
| Web 2    |  Web Server        |  10.0.0.6  |  Ubuntu  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Machines within the network can only be accessed by the JumpBox (10.0.0.4)


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box    | Yes/Port 22  | 10.0.0.1 10.0.0.2   
|   Web 1& 2  |    No             |             
|  LoadBlncr   |   Yes/80       | 13.86.215.2  
| Elk               |  Yes/5601    |  *     

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows for full automation of a specific server and reduces configuration errors.

The playbook implements the following tasks:

Install Docker: Installs the core docker code to the remote server
Install Python3_pip: Pip is an installation module that allows for additional docker modules to be installed easier
Docker Module: Tells the previous PIP module to install the necessary docker component modules
Increase Memory/Use More Memory: A common issue with the ELK Docker image is to little memory. This help fix the issue to allow the server to launch
Download and Launch ELK Container: This downloads the ELK docker container and initializes it with the specified ports being published


### Target Machines & Beats
This ELK server is configured to monitor the following machines:

10.0.0.4
10.0.0.5
10.0.0.6

We have installed the following Beats on these machines:

Filebeat & Metricbeat
These Beats allow us to collect the following information from each machine:
Filebeat: collects system type events such as logins to see who is actively logging into the system.

Metricbeat: collects useful information such as cpu usage and memory, this is particularly useful when seeing if there are any programs or concerning behaviors taking system resources


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml.
- Update the hosts file to include the attribute, such as elk, then include your destination IP of the Elk Sever
.
- Run the playbook, and navigate to http://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.

### Commands used to download playbook & update files

On the Jump box run the following command to get the playbook: curl /etc/ansible/roles/elk_install.yml
Edit the host file in /etc/ansible as follows:

[elk]
10.1.0.4	ansible_python_interpreter=/usr/bin/python3

Run: ansible-playbook /etc/ansible/roles/elk_install.yml
Check your installation is working by visiting in a browser: http://[your_elk_server_ip]:5601/app/kibana
### Installing Filebeats

Download the playbook with the following command: curl /etc/ansible/roles/filebeak_playbook.yml

Run the playbook with: ansible-playbook /etc/ansible/roles/filebeat_playbook.yml
