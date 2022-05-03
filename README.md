# Elk-Stack
The files in this repository were used to configure the network depicted below.

[Elk-Stack Diagram](

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  installelk-playbook.yml 

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build

### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly distributed, in addition to restricting unwanted traffic to the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log file data and system metrics.

The configuration details of each machine may be found below.

| Name       | Function     | IP Address | Operating System |
|------------|--------------|------------|------------------|
| Jump Box   | Gateway      | 10.0.0.1   | Linux            |
| Elk-Server | Monitor Data | 10.1.0.4   | Linux            |
| Web-1      | Host DVMA    | 10.0.0.8   | Linux            |
| Web-2      | Host DVMA    | 10.0.0.9   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisoner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
    
  **108.48.194.72**
     
Machines within the network can only be accessed by JumpBoxProvisoner. 
  
  JumpBoxProvisoner IP:
 
  **10.0.0.4**
 

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses |
|------------|---------------------|----------------------|
| Jump Box   | Yes                 | 108.48.194.72        |
| Elk-Server | No                  | 10.0.0.4             |
| Web-1      | No                  | 10.0.0.4             |
| Web-2      | No                  | 10.0.0.4             |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the use of automating configuration reduces repetitve tasks and allows team members to focus on projects rather than spend time on documenting log data.    

The playbook implements the following tasks:

- Install docker.io, python3-pip, docker module
- Increases virtual memory 
- Download and launch a docker Elk container on specficied ports 

	**5601**
  
  **9200**
  
	**5400**
  
- Enable service docker on boot   

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

[Docker ps Result](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.8
- 10.0.0.9

We have installed the following Beats on these machines:
- Filebeat
- MetricBeat

These Beats allow us to collect the following information from each machine:

Fliebeat: colllects data about file systems which is used to track log data, which is then centralized to Logstash. This allows us to collect log data such as system.log and keep the data in one place. 

Metricbeat: collects machine and hardware mertics like uptime or CPU usage. This allows us to monitor machine preformance to make sure the hardware is running correctly.   

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the installelk-playbook.yml file to roles directory.


  `cp installelk.yml roles`
  
  
- Update the hosts file to include which machines you want to run the playbook on then follow these commands

	 
   1.`cd /etc/ansible`
   
   2.`nano hosts`

  
	3.Scroll in the hosts file for [webservers] group and add your machines you want the playbook to run on then add these comments:
	```
  	[webservers]
    10.0.0.8 ansible_python_interpreter=/usr/bin/python3   
    10.0.0.9 ansible_python_interpreter=/usr/bin/python3
	```
	4.While still in hosts file find or create an [elk] group and add your machine you want the elk server to run on then add these comments:
		  
      [elk]
      10.1.0.4 ansible_python_interpreter=/usr/bin/python3

- Run the playbook, and navigate to http://yourelkserverpublicip:5601/app/kibna to check that the installation worked as expected.

