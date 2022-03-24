# ELK-Stack-Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

<img src="https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-TrunkMonk/blob/main/images/AzureDockerELKstack.png" style="max-width: 100%;"/>

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ELK Install Playbook file may be used to install only certain pieces of it, such as Filebeat.

  <a href="https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-TrunkMonk/blob/main/playbooks/install-elk.yml">ELK Install Playbook</a></br>
  <a href="https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-TrunkMonk/blob/main/playbooks/filebeat-playbook.yml">Filebeat Install Playbook</a></br>
  <a href="https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-TrunkMonk/blob/main/playbooks/metricbeat-playbook.yml">Metricbeat Install Playbook</a></br>

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the web application will be highly available, in addition to restricting access to the network.
- In addition to high availability and access restriction, load balancers also help to mitigate Distributed Denial of Service (DDoS) attacks by detecting and dropping traffic before it reaches web servers. Load balancers improve the efficiency of content delivery by distributing the load across multiple web servers while also providing resiliency and scalability of web server pools.
- A Jump Box acts as a gateway to provided highly restricted ingress access to the corporate network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system metrics.
- Filebeat watches for changes in log files
- Metricbeat records related datasets and system metrics from servers or services

The configuration details of each machine may be found below.

| **Name** | **Function** | **IP Address** | **Operating System** |
|----------|--------------|----------------|----------------------|
| Jump Box | SSH Gateway  | 10.0.0.4       | Linux Ubuntu 18.04   |
| Web-1    | Web server   | 10.0.0.5       | Linux Ubuntu 18.04   |
| Web-2    | Web server   | 10.0.0.6       | Linux Ubuntu 18.04   |
| Web-3    | Web server   | 10.0.0.7       | Linux Ubuntu 18.04   |
| ELK      | ELK Stack    | 10.1.0.4       | Linux Ubuntu 18.04   |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- My public IP address

Machines within the network can only be accessed by the Jump Box.
- Only my public IP address is permitted to access the public IP of the ELK VM on port 5061.

A summary of the access policies in place can be found in the table below.
| **Name**      | **Publicly Accessible** | **Allowed IP Address** |
|---------------|-------------------------|------------------------|
| Jump Box      | Yes                     | My Public IP Address   |
| Web-1         | No                      | 10.0.0.0/24            |
| Web-2         | No                      | 10.0.0.0/24            |
| Web-3         | No                      | 10.0.0.0/24            |
| Load Balancer | Yes                     | Any                    |
| ELK           | Yes                     | My Public IP Address   |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it produces replicable and consistent results across one or many deployments.

The playbook implements the following tasks:
- Downloads and installs Docker and Python3-pip
- Configures the ELK VM to use more memory
- Enables the Docker service, downloads the ELK image, launches the ELK container, opens ports 5061, 9200 and 5044, and sets the restart policy to always

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

<img src="https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-TrunkMonk/blob/main/images/docker_ps_output.png" style="max-width: 100%;"/>

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- Web-3 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat - When installed on a machine, Filebeat collects log files on the host then forwards the data to Logstash for processing.  For example, we can use Filebeat to gather authentication logs from the file system to more easily analyze the volume, frequency, source location, successes, and failures of SSH logins to a monitored host.
- Metricbeat - When installed on a machine, Metric beat collects machine metrics such as uptime, service and system performance and sends this data to Logstash for processing.   Some of the metrics we might expect to see are the number of Docker containers on a machine, their memory usage, CPU usage, network and disk IO.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to the Ansible control node.
- Update the /etc/ansible/hosts/hosts.yml file to define the IPs of the webservers, add an [elk] group, and specify the IP address of the ELK VM you created in Azure
<img src="https://github.com/UCB-CyberSecurity-Cohort5/elk-stack-project-TrunkMonk/blob/main/images/Ansible_hosts_file.png" style="max-width: 100%;"/>

- Run the playbook, and navigate to the http://ELKVM-PUBLIC-IP:5061 to check that the installation worked as expected.
- The playbook is install-elk.yml and should reside in /etc/ansible/ on Ansible Control node
- The playbook will run against the groups defined /etc/ansible/hosts/hosts.yml, where IP addresses for each group are recorded.
- To check that your ELK server is running, navigate to http://ELKVM-PUBLIC-IP:5061

### Commands to Download the Playbook, Update the Files and Run the Playbook
- 
