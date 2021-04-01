## Automated ELK Stack Deployment
The files in this repository were used to configure the network depicted below.
![Network_Topology](https://github.com/NoobiusDorkius/UCSDproject1/blob/main/Diagrams/Project1%20topology.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the YAML file may be used to install only certain pieces of it, such as Filebeat.

![Main_YAML_Playbook](https://github.com/NoobiusDorkius/UCSDproject1/blob/main/Ansible/Playbook.txt)


This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology
The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be **highly Available**, in addition to restricting **Unauthorized users** to the network.

What aspect of security do load balancers protect? What is the advantage of a jump box?

-AVAILABILITY from the CIA Traid
-Single point of secured entry to prevent unauthorized access and administer commands to the rest of the VNET

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the **protected folders** and system **log files**.

What does Filebeat watch for?

-Changes to log files and protected files

What does Metricbeat record?

-Spikes or dramatic changes to system resources including processor

The configuration details of each machine may be found below.

| Name    | Function    | IP Address | Operating System |
|---------|-------------|------------|------------------|
| JumpBox | Gateway     | 10.0.0.1   | Linux (Debian)   |
| Web-1   | Aggregation | 10.0.0.4   | Linux (Debian)   |
| Web-2   | Aggregation | 10.0.0.5   | Linux (Debian)   |
| ELK-Net | SIEM        | 10.1.0.4   | Linux (Debian)   |

### Access Policies
The machines on the internal network are not exposed to the public Internet. 
Only the **JumpBox** machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

-162.230.224.69

Machines within the network can only be accessed by **ME.**

A summary of the access policies in place can be found in the table below.

| Name    | Publicly Accessible | Allowed IP              |
|---------|---------------------|-------------------------|
| JumpBox | Yes                 | 162.230.224.69          |
| Web-1   | No                  | 10.0.0.1                |
| Web-2   | No                  | 10.0.0.1                |
| ELK-Net | Yes                 | 162.230.224.69/10.0.0.1 |

### Elk Configuration
Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...

-It can easily be duplicated and remotely automated without user interaction

The playbook implements the following tasks:

-Install Docker.io
-Install docker dependancies for containers
-Install ELK container
-expand memory to match minimum required to function
-host Kibana dashboard for additional configuration

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
![Docker_PS_Output](https://github.com/NoobiusDorkius/UCSDproject1/blob/main/Linux/docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web-1 && Web-2
- 
We have installed the following Beats on these machines:

-Filebeat && Metricbeat

These Beats allow us to collect the following information from each machine:

-Filebeat allows us to collect information about changes or alteration to protect files and directories including "auth.log"

-Metricbeat monitors resource usage for increases or sudden spikes in usage similar to those caused by a brute force attack or C2C communication

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 
SSH into the control node and follow the steps below:
- Copy the **Config** file to **Target VM**.
- Update the **Hosts** file to include IP address of additional VM to webservers group
- Run the playbook, and navigate to **newly configured VM** to check that the installation worked as expected.

Which file is the playbook? Where do you copy it?

-The YAML file and it should be copied to a general playbook directory within /etc/ansible

Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?

-You start by updating the hosts file. in the playbook you call a host in the second line of the file to specify which machine to install to.

Which URL do you navigate to in order to check that the ELK server is running?

-The ELK server's public IP address

As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc.

-cat the playbook template and copy contents -- paste in a new file with nano > ctrl + shift + V and save as a yml extention -- modify hosts to reflect IP (private) -- run the command "ansible-playbook" and the name of the new yml file -- sit back and watch like a mad scientist
