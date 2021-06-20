## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

https://github.com/farinainna21/cybersecurity/blob/main/Diagram/Screenshot%202021-05-20%20141727.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

  - (Playbooks/install-elk.yml) (Playbooks/filebeat-playbook.yml)



This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly _____, in addition to restricting _____ to the network.
-What aspect of security do load balancers protect? What is the advantage of a jump box?_
The Jump Box serves as the gateway to the virtual network. This allows the administrator the ability to have remote access capability.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the uptime_____ and system  logs_____.
 What does Filebeat watch for?_     Filebeat is deployed on VMs in the environment in order to monitor all the system logs that are being generated.

 What does Metricbeat record?_   Although Metricbeat was not deployed for this current build it is certainly on the short list for furture enhancements. Metricbeat records uptime and system metrics based around the VMs perfomrace related to the CPU, memory, etc.

If the pool of VMs begins to grow adding a load balancer will ensure that the application will be highly stable with the increased traffic. The load balancer will also help keep the network's availability high with routing traffic evenly across the networks.

 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 20.37.46.129   | Linux            |
| DVWA-VM1   File beat ||13.73.117.182 |                  |
| ELK     | ELK SERVER |10.1.0.4   |                  |
| TODO     |          |            |                  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the ___jump Box__ machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _20.37.46.129 Add whitelisted IP addresses_

Machines within the network can only be accessed by _local workstation and jumpbox____.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?          Jumpbox VM: IP 10.0.0.4 Local Workstation via SSH IP 96.48.81.73

_

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes  |              | 20.37.46.129
| project1  |No   |              | 10.1.0.4
|   web1    |NO   |              | 10.0.0.5


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_ Install docker.io
The playbook implements the following tasks:

Install docker.io
name: Install docker.io apt: update_cache: yes name: docker.io state: present
Install Python-pip
name: Install pip3 apt: force_apt_get: yes name: python3-pip state: present
Install: docker
name: Install Docker python module pip: name: docker state: present
Command: sysctl -w vm.max_map_count=262144
Launch docker container: elk
name: download and launch a docker elk container docker_container: name: elk image: sebp/elk:761 state: started restart_policy: always published_ports: - 5601:5601 - 9200:9200 - 5044:5044
The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.

Diagrams/dockerps.PNG



The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://github.com/farinainna21/cybersecurity/blob/main/Diagram/docker.PNG

### Target Machines & Beats
This ELK server is configured to monitor the following machines

Project1 10.1.0.4
Web-1, 10.0.0.5
Web-2, 10.0.0.6


We have installed the following Beats on these machines:
- Filebeats
Metricbeats

These Beats allow us to collect the following information from each machine:
- Filebeat collects system logs, which can be used to track system events, etc.
Metricbeat collects system and service metric data, which we can use to see CPU usage, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat file and Metricbeat  /etc/ansible/[your_dir]/[your-file-name].
- Update the config file to include your ELK-server's private IP address. (filebeat-config.yml: lines 1106 & 1806, metricbeat-config.yml: lines 62 & 96)
- Run the playbook, and navigate to http://[ELK-server-public-IP]:5601/app/kibana to check that the installation worked as expected__ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
/etc/ansible/roles/filebeat-playbook.yml is the filebeat playbook. 


- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
/etc/ansible/files/metricbeat-playbook.yml is the metricbeat playbook. Copy it to /etc/ansible/[your_dir]/[your-playbook-name]
- _Which URL do you navigate to in order to check that the ELK server is running?
To make Ansible run the playbook on a specific machine(s), update the /etc/ansible/hosts file. Within this file, name groups using square brackets (currently contains '[webservers]' and '[elk]') surrounding the group-name and under the group-name, replace private IP's with your own respective IP's. You then use these group-names behind the "hosts:" field in the playbooks to specify which machines to apply the playbook to.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
To confirm the ELK-server is running go to http://[ELK-server-public-IP:5601]/app/kibana

