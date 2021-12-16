## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](https://user-images.githubusercontent.com/88005785/145894794-3fb4d754-f67e-4e52-a754-9b76416248b3.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Ansible and ELK playbook files may be used to install only certain pieces of it, such as Filebeat.

  - [install-elk.yml](C:\Users\Nanneys\Azure-Virtual-Network-with-ELK-Deployment\Ansible\install-elk.yml)
  - [filebeat-playbook.yml](C:\Users\Nanneys\Azure-Virtual-Network-with-ELK-Deployment\Ansible\filebeat-playbook.yml)
  - [metricbeat-playbook.yml](C:\Users\Nanneys\Azure-Virtual-Network-with-ELK-Deployment\Ansible\metricbeat-playbook.yml)

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
- What aspect of security do load balancers protect? By ensuring high availability, load balancers seek to protect networks against system unavailability through attacks such as distributed denial-of-service (DDoS) attacks.
- What is the advantage of a jump box? A jump box provides system administrators with a remote origination point for secure and segregated access to a network for the purpose of completing administrative tasks.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the config and system log files.
- What does Filebeat watch for? Filebeat watches for log data in specific files, such as logs generate by Apache and Azure tools. This log data is collected and aggregated from remote machines and the aggregated data is sent to output configured in Filebeat.
- What does Metricbeat record? Metricbeat records metrics from the operating system and from services running on the server.

The configuration details of each machine may be found below.

| Name               | Function   | IP Address                             | Operating System     |
|--------------------|------------|----------------------------------------|----------------------|
| JumpBoxProvisioner | Gateway    | 10.0.0.4(Private)/20.121.17.211(Public)| Linux (ubuntu 18.04) |
| VM2                | Web Server | 10.0.0.5(Private)                      | Linux (ubuntu 18.04) |
| VM3                | Web Server | 10.0.0.6(Private)                      | Linux (ubuntu 18.04) |
| VM4                | Web Server | 10.0.0.7(Private)                      | Linux (ubuntu 18.04) |
| ELKServer          | ELK Server | 10.2.0.4(Private)/40.69.184.112(Public)| Linux (ubuntu 18.04) |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the JumpBoxProvisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 98.253.33.224

Machines within the network can only be accessed by JumpBoxProvisioner.
- Which machine did you allow to access your ELK VM? Only the JumpBoxProvisioner has access to the ELKServer.
- What was its IP address? 20.121.17.211

A summary of the access policies in place can be found in the table below.

| Name               | Publicly Accessible | Allowed IP Addresses |
|--------------------|---------------------|----------------------|
| JumpBoxProvisioner | Yes                 | 98.253.33.224        |
| VM2                | No                  | Via LB: 20.39.40.105 |
| VM3                | No                  | Via LB: 20.39.40.105 |
| VM4                | No                  | Via LB: 20.39.40.105 |
| ELKServer          | No                  | None                 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because manual configurations are time and resource intensive and can lead to configuration errors.
- What is the main advantage of automating configuration with Ansible? The main advantage of automating configuration with Ansible is that Ansible allows for the automatic deployment of complex configurations on a system wide basis. 

The playbook implements the following tasks:
- Installs Docker
- Installs Python3_pip
- Increases virtual memory for ELK deployment
- Downloads and launches a Docker ELK container
- Enables Docker service to launch on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](https://user-images.githubusercontent.com/88005785/145894999-7ab5d516-f459-4594-9e32-b744187c86b4.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- VM2 - 10.0.0.5
- VM3 - 10.0.0.6
- VM4 - 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat: [module status](https://user-images.githubusercontent.com/88005785/145895061-47b9e0c1-fa92-44a7-8eb1-d935c86560db.png)
- Metricbeat: [module status](https://user-images.githubusercontent.com/88005785/145895094-a0616b46-6ae4-4e3e-a1c1-90caa784cb40.png)

These Beats allow us to collect the following information from each machine:
- Filebeat allows us to collect and ship log files. For example, Filebeat can collect deprecation logs. It is important to monitor deprecation logs to ensure we are working with the current versions of applications and services, including those in the ELK stack.
- Metricbeat allows us to collect server data on a system-wide and per-process CPU. This information is important for monitoring CPU, memory and disk usage and the overall performance of the network.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the install-elk.yml file to /etc/ansible/roles/install-elk.yml.
- Update the hosts file to include the attributes of the ELK VM in order for Ansible to discover, connect to and configure this machine.
- Run the playbook, and navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana to check that the installation worked as expected.


To download the playbooks, update the files, running the installations and launch the services, from the directory of the location of the file, or with the specific filepath, from the command line, enter "ansible-playbook [yml playbook name]
