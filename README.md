## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/NetworkDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select yml files may be used to install only certain pieces of it, such as Filebeat.

  - install-elk.yml
  - filebeat-playbook.yml
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

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

The Jump Box protects the confidentially of the network by only allowing ssh access via the one machine. In addition to this, should settings on the webservers need to be changed or updated we only need to makes changes on the Jump Box.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system services.

The configuration details of each machine may be found below.


| Name         | Function   | IP Address | Operating System      |
|----------    |----------  |------------|------------------     |
| Jump Box     | Gateway    | 10.0.0.4   | Linux (ubuntu 18.04)  |
| Web-1        | Webserver  | 10.0.0.5   | Linux (ubuntu 18.04)  |
| Web-2        | Webserver  | 10.0.0.6   | Linux (ubuntu 18.04)  |
| Web-3        | Webserver  | 10.0.0.8   | Linux (ubuntu 18.04)  |
| ELKserver    | ELKserver  | 10.1.0.4   | Linux (ubuntu 18.04)  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBox machine can accept ssh connections and the Load Balancer http requests. Access to these machines is only allowed from the following IP addresses: 122.111.26.70

Machines within the network can only be accessed by the Jump Box or the Load Balancer

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessible  | Allowed IP Addresses     |
|-------------- |--------------------- |------------------------- |
| Jump Box      | Yes                  | 122.111.26.70            |
| Webservers    | No                   | 10.0.0.4, load balancer  |
| ELKserver     | Yes                  | 122.111.26.70            |
| Load Balancer | Yes                  | 122.111.26.70            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it is scaleable if want to setup multiple machines.

The playbook implements the following tasks:

- Install docker module
- Increase memory
- Download and launch a docker elk container
- Check the docker service is running

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1
- Web-2
- Web-3

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeats collects logfile data and ships it to the ELK stack for analysis, which we use to track which files were downloaded and metricbeats ships host metrics such as system services, which we can use to track CPU and memory usage.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to your ansible container
- Update the /etc/ansible/hosts file to include the private ip addresses of your webservers and ELK server
- Run the playbook, and navigate to [ELKserverip]:5601 to check that the installation worked as expected.
