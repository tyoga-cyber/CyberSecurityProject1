## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK file may be used to install only certain pieces of it, such as Filebeat.
                                                                                                                                                           
  * ELK install
  * DVWA
  * Filebeat
  * Metricbeat

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


A load balancers are placed in front of your servers and is an efficient distribution of traffic across multiple servers.  The purpose is to route requests across all servers capable fulfilling  them while optimizing maximum speed and capacity utilization. By doing so, it would ensure no one service is overworked and distributed the requests.


The use of a jump box is to act as a point of entry for administrators accessing critical systems and where all administrative actions performed via a jump box.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system effectiveness.


The purpose of Filebeat is to assist in monitoring log files or focus on specific locations which are specified, collects log events, and forwards them either to Elasticsearch or Logstash for indexing/analyzing.

Metricbeat collect metrics from the operating system as well as services running on the server displayed on ElasticSearch

The configuration details of each machine may be found below.


| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Ubuntu           |
| WEB 1    | Server   | 10.0.0.5   | Ubuntu           |
| WEB 2    | Server   | 10.0.0.6   | Ubuntu           |
| WEB 3    | Server   | 10.0.0.7   | Ubuntu           |    
| ELK      | ELK STACK| 10.1.0.4.  | Ubuntu           |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

142.122.123.31

Machines within the network can only be accessed by the Jump Box.
The ELK machine can only be accessed by the Jump Box via the IP Addresses below:
- Public IP 52.170.115.182
- Private IP 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses     |
|----------|---------------------|--------------------------|
| Jump Box | Yes                 | 142.122.123.31/32        |
| WEB 1    | NO                  | 10.0.0.4/32, 40.88.2.227 |
| WEB 2    | NO                  | 10.0.0.4/32, 40.88.2.227 |
| WEB 3    | NO                  | 10.0.0.4/32, 40.88.2.227 |
| WEB LB   | YES VIA PORT 80 HTTP|           *              |
| ELK      | YES VIA PORT 5601   | 142.122.123.31/32        |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it uses simple language which allows for easily deployed automation jobs.  It creates efficiencies, ensures security and provides the ability for larger scale tasks.


The playbook implements the following tasks:

- Install docker.io.   It would install the docker container
- Install python3-pip. It would retrieve a pre-package-management system written in Python used to install and manage software packages. 
- Install Docker module. This would install, configure and manages Docker from the Docker repository.
-Download and Launch ELK Container This downloads the ELK docker container and launches it with the specified ports being published

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

| Name  |  Server   |
|-------|-----------|
| WEB 1 | 10.0.0.4  |
| WEB 2 | 10.0.0.5  |
| WEB 3 | 10.0.0.6  |


We have installed the following Beats on these machines:

| Name  | Name of Beat installed |
|-------|------------------------|
| WEB 1 | Metricbeat             |
| WEB 2 | Metricbeat             | 
| WEB 3 | Metricbeat             |
| Elk   | Filebeat               |

These Beats allow us to collect the following information from each machine:
 
Filebeats collects and analyzes logs from Docker containers.

Metricbeat gathers specific metric data from servers.

### Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

Copy the elk install.yml file to /etc/ansible/.

Update the configuration file to include the elk server ip..


Run the playbook, and navigate to http://[elkserverip]:5601/app/kibana#/home to check that the installation worked as expected.


_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

On the Jump box run the following command to get the playbook: 

Edit the hosts file in /etc/ansible/hosts and add the details from the

The command to run the Playbook: ansible-playbook /etc/ansible/elk_install.yml

Check your installation is working by visiting in a browser: http://[your_elk_server_ip]:5601/app/kibana

You should see something similar to this:

Installing Filebeats:

Download the playbook with the following command: 

Run the playbook with: ansible-playbook /etc/ansible/roles/filebeat_playbook.yml

You should begin seeing information such as the following:
