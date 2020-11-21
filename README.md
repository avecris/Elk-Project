# Elk Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[Network Diagram](images/Network-Diagram.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

  -[Webserver Playbook](Webserver-Playbook)
  
  -[Elkserver Playbook](Elkserver-Playbook)
  
  -[Filebeat Playbook](Filebeat-Playbook)
  
  -[Metricbeat Playbook](Metricbeat-Playbook)

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
- Load balancers make controlling access to a network easier, by making traffic directed to the webservers pass through one machine.  This means that security controls put onto the load balancer ensure that all the machines behind it are protected.  This is an advantage of only allowing SSH access to the machines via a single 'Jump Box' machine.  As long as you properly control access to the jumpbox, you control access to all the machines behind it._

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the permissions and system files.
- Filebeat collects log files on a machine and sends them on to a system that can collect and analyse them.
- Metricbeat collects metrics system metrics like CPU usage and disk usage and also forwards them on to a system which can collect and analyse the data.

The configuration details of each machine may be found below.
| Name       | Function            | IP Address | OS    |
|------------|---------------------|------------|-------|
| Jump Box   | Gateway             | 10.0.0.4   | Linux |
| Web 1      | Hosts Website       | 10.0.0.5   | Linux |
| Web 2      | Hosts Website       | 10.0.0.6   | Linux |
| Elk Server | Monitors webservers | 10.1.0.5   | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Load balancer accepts HTTP connections from the Internet.  However, the Jump box machine accepts ssh connections over the internet, and the Elk Server accepts http connections via port 5601. 
- 1.136.108.44

Machines within the network can only be accessed by the Jump Box.
- I only allowed the Jump Box machine to provide ssh access to the Elk Server.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses                     |
|------------|---------------------|------------------------------------------|
| Jump Box   | Yes                 | 10.0.0.5 10.0.0.6 1.356.108.144          |
| Web 1      | No                  | 10.0.0.4 10.1.0.5                        |
| Web 2      | No                  | 10.0.0.4 10.1.0.5                        |
| Elk Server | Yes                 | 10.0.0.4 10.0.0.5 10.0.0.6 1.356.108.144 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it allows the process to be easily repeatable without errors.  

The Elkserver playbook implements the following tasks:
- Installs the Docker service
- Installs the Python3-Pip service
- Installs a Docker Module onto the container
- Changes the value vm.max_map_count in the systemctl configuration file to "262144"
- Downloads and launches the image of a Docker container
- Enables the Docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Screenshot after running `docker ps`](images/Elk-Server-Container)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web 1: 10.0.0.5
- Web 2: 10.0.0.6

We have installed the following Beats on these machines:
- Web 1: 10.0.0.5
- Web 2: 10.0.0.6

These Beats allow us to collect the following information from each machine:
- FileBeat collects log files from the machine it runs on.  An example of a type of log file is system logs, which contain information about changes made to the operating system)  While MetricBeat collects system metric data.  This is data concerning the OS, such as OS disk usage, memory usage, CPU usage, etcetera.
### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the Playbook files to /etc/ansible.
- Update the hosts field of the playbook files to tell Ansible which groups of host machines to run the playbook on
- Run the playbook, and navigate to http://<IP address of your Elk Server>/app/5601 to check that the installation worked as expected.

