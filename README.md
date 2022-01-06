## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)
/Users/juliajones/Documents/GitProjects/CyberSecurity/CyberSecurity/Diagrams/Cloud_Security_Diagram.jpg

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the Playbook yaml file_____ file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._
  
  /CyberSecurity/Ansible/install-elk.yaml
  
This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.
Load balancing ensures that the application will be highly availible , in addition to restricting traffic to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_
Load balancers protect the access and load of web servers. When under heavy traffic load balancers distribute the traffice to multiple machines in order to allow access to requesters and not overburden one server.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the virtual machines and system newtork.
- _TODO: What does Filebeat watch for?_
        Filebeat is a lightweight log snipper. This allows for a user to centralize and monitor log data. This data can then sent to other services such as logstash for indexing. This is helpful in identifying irregular patterns in log data that could indicate a breach in security.
- _TODO: What does Metricbeat record?_
    Metricbeat is a lightwieght log snipper that periodically  collect metrics for operating systemsand other services specified on a server. This data then can be sent to services such as logstash for further indexing. These metric and statistics can be collected from a wide variety of services that can be used to determine the known behaviour and efficeincy of services and identify irregualrities. 

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name        | Function          | IP Address | Operating System |   |
|-------------|-------------------|------------|------------------|---|
| Jump Box    | Gateway           | 10.1.0.4   | Linux            |   |
| Web-1       | DVWA              | 10.1.0.5   | Linux            |   |
| Web-2       | DVWA              | 10.1.0.6   | Linux            |   |
| Elk-machine | Kibana app server | 10.2.0.4   | Linux            |   |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_
 73.34.178.176 Home IP address

Machines within the network can only be accessed by JumpBox machine.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_
The Jump box virtual machine using network peering , 10.1.0.4 is the Interal Ip and the public IP is 52.249.193.165

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes/No              | 10.0.0.1 10.0.0.2    |
|          |                     |                      |
|          |                     |                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _TODO: What is the main advantage of automating configuration with Ansible?_
Ansilbe can configure multiple  machines at once. Instead of individually configuring each machine, Ansible allows one user to write a playbook on machine configuration and use it to automate multiple machines at any time greatly increasing efficientcy. 

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...
In the Elk installation Playbook Yaml file the firs step is to use the apt module to install docker.io onto the virtual machine. 
Then it will also python3-pip in order to run python scripts. Once that is done Docker module will be installed using a pip method. 
Then using the command module the system control will set its maxium memory allowance.

Then the docker conatiner will be installed and lauched. The image name will be sebp/elk:761, which will always e restarted and the allowed ports of 5601, 9200 , and 5044.

Finally , the docker service on the machine will be enable on boot.

- ...

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)
/Users/juliajones/Documents/GitProjects/CyberSecurity/CyberSecurity/Images/Docker_ps_output.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
10.1.0.5
10.1.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

We installed Filebeat and Metricbeat.

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

Filebeat collects logs lines using harvesters. THe Harvesters read the file line by line and output the logs lines to other services such as elastic search. Filebeat could output logs data such as the timestamp of when the log was sent e.g. Jan 5, 2022 @ 23:25:14.000.

Meticbeat collects log metric data about the services it is monitoring. Metric beat can record how much system memorey percenatage a service has used. e.g system.process.memory.rss.pct:4.94% .

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ install- file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
Install-elk.yaml at the given file /Resources/install-elk.yml

A Yaml file is usualy the playbook file. Playbook files created can follow the template ""-playbook.yml. Several yaml files provided will  use this template.
The playbook is placed in the etc/ansible folder of the ansible control node.
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
You have to update the etc/ansible/hosts file by including the group and ip address which the playbook file will apply the instructions.
- _Which URL do you navigate to in order to check that the ELK server is running?
You need to use the configured public IP address in azure and port 5601.
http://`[Public IP Addresss of Elk machine]`:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._

