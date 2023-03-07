# ELK Project
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.
_*Refer to Cloud Virtualization within /Diagrams*_

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yml and config file may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - filebeat-config.yml
  - filebeat-playbook.yml
  - metricbeat-config.yml
  - metricbeat-playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting access to the network.

- What aspect of security do load balancers protect? What is the advantage of a jump box?
Load balancers mainly serve to protect organizations against distributed denial-of-service, or DDoS attacks. They do this by evenly 
distributing web traffic amongst multiple servers and enabling threat intelligence based filerting at the firewall, alerting when malicious 
IP addresses are attempting communication. Load balancers are typically placed behind the firewall or router, balancing the
servers behind it, protecting resources and web applications within the network. 
Additionally, load balancers provide support such as, (but not limited to):

	- upholding network security group rules created for backend and outbound traffic 
	  belonging to virutal networks, subnets and NICs
	- logging and monitoring of traffic carried through virtual networks and subnets
	- sustain network-based IDPS and IDPS, intrusion detection and prevention systems
	- tools that allow monitoring for resource configurations and modifications to internal resources

- What is the advantage of a jump box?
The advantage of having a jump box is an increased level of security. It servers as a gateway, or bridge, between two network zones and enables
access and mangement of the devices located in the VM. To prevent public exposure of the VM, the public IP addfress can refuse connection, adding 
a layer of protection to the VM itself.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file system and system metrics.
- The Filebeat monitors log files or locations that we've specified. It collects log events and forwards them to Logstash for indexing.
- The Metricbeat records metrics and statistics that collects and transfers them to the output specified. It also helps mointor servers
 by collecting metrics from the system and services running over the server.

The configuration details of each machine may be found below.

| Name       | Function      | IP Address             | Operating System |
|------------|---------------|------------------------|------------------|
| JumpBox    | Gateway       | 20.211.12.52, 10.0.0.7 | Linux            |
| Web-1      | VM/Webserver  | 13.75.137.75, 10.0.0.5 | Linux            |
| Web-2      | VM/Webserver  | 13.75.137.75, 10.0.0.6 | Linux            |
| ELK        | Kibana        | 20.89.180.32, 10.1.0.4 | Linux            |
| RedTeam-LB | Load Balancer | 13.75.137.75           | DVWA             |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 96.41.45.5

Machines within the network can only be accessed by the jumpbox.
- Jumpbox
	- Public IP: 20.211.12.52
	- Private IP: 10.0.0.7

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP Addresses |
|---------|---------------------|----------------------|
| JumpBox | Yes                 | 96.41.45.5           |
| ELK     | Yes                 | 10.1.0.0/24          |
| DVWA 1  | No                  | 10.0.0.1-254         |
| DVWA 2  | No                  | 10.0.0.1-254         |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because
Ansible doesn't require coding on any level to use or create the playbooks. It not only can configure new machines, but can do so for
many servers at a time, updating programs, automating tasks and create environments regardless of its placement.

- What is the main advantage of automating configuration with Ansible?
Ansible automates IT environments hosted in several environments such as bare metal machines, virtual platforms or cloud based services. 
It's capable of configuring devices such as databases, networks, firewalls and databases.

The playbook implements the following tasks:
- Uses the following modules:
   - docker.io
   - python3-pip
   - Docker module
- Uses and increases virtual memory
- Download and launch a docker elk container
- Enables service Docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
_*Refer to ELK docker within /Diagrams/Images*_


### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1/DVWA 1 - 10.0.0.5
- Web-2/DVWA 2 - 10.0.0.6

We have installed the following Beats on these machines:
- Metricbeats
- Filebeats

These Beats allow us to collect the following information from each machine:
- Metricbeat collects metrics and statistics from the systems and services we've configured on our server. That data is then complied and deployed for viewing directly on Elasticsearch or sent to 
Logstash, Redis or Kafka. With Metricbeats we expect to see a collection consisting of CPU metrics, memory or data related to running services.
- Filebeat is another lightweight shipper that performs different tasks than Metricbeat. Filebeat will centralize log data according to user specified files, and forward them to Elasticsearch or Logstash.
Filebeat can be helpful in situations where there are network interruptions by picking up the last successfully indexed line in the log and resuming connection.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy install-elk.yml to /etc/ansible/install-elk.yml
- The hosts file gets updated to ensure Ansible runs the playbook by specifying [elk] as an attribute, then insert the IP address of the ELK server.
- Navigate to http://[your.VM.IP]:5601/app/kibana, using the public IP address of the ELK server to ensure the ELK server container is up and running.


Here are specific commands a user will need to run to download the playbook, update the files, etc.
- ssh jumpbox@IP_address
- docker run -ti container/ansible
- change dir. /etc/ansible
- ssh-keygen to your web server
- go to nano hosts and update the IP for webservers and elk
- edit the nano ansible.cfg and change the remote_user to the server you want to use












