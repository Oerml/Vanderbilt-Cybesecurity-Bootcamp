## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted in Elk Stack, in the Diagrams folder

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

  - The ansible-playbooks install-elk.yml, metric-playbook.yml, and filebeat-playbook.yml are needed to create and implement the elk-server

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly redundant, in addition to restricting traffic to the network.
- Loab balncers protect the system from DDoS attacks by shiffting attack traffic, and a jump box is to give access to the user from a single node that can be secured and monitored

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat watches for logfiles/locations and collects log events
- Metricbeat records metric and statistical data from the operating system and from services running on the server

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| web1     | Docker   | 10.0.0.7   | Linux            |
| web2     | Docker   | 10.0.0.6   | Linux            |
| web3     | Docker   | 10.0.0.8   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 68.52.216.11

Machines within the network can only be accessed by ssh.
- the only machine that is able to connect to the elk server 10.1.0.5 is via jumpbox private ip 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses   |
|----------|---------------------|------------------------|
| Jump Box | no                  | Personal IP only       |
| web1     | no                  | 10.0.0.4               |
| web2     | no                  | 10.0.0.4               |
| web3     | no                  | 10.0.0.4               |
| elk      | no                  | 10.0.0.4 & Personal IP |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The main advantages of automating a configuration through Ansible is the ease of use and extremely easy learning curve. The ability to use Playbooks makes the configuration of multiple machines through one single command

The playbook implements the following tasks:
- Create a new vm, keep note of the public and private IP, connect to kibana portal to measure metrics
- download and configure the elk-docker, in adition add elk under webservers in the config file, and map elk to the ports 5601,9200,5044
- laucnh and expose the container, connect via ssh

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- [10.0.0.7, 10.0.0.6, 10.0.0.8]

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is a lightweat shipper for forwarding and centralizing log data. Filebeat monitors logs, collects log events, then forwards them to elasticsearch or logstash
- Metricbeat collects metrics from the operatin system and from servies running on the server. Metricbeat takes These metrics and stats and ships them to an out you specify

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the filebeat-playbok.yml and metric-playbook.yml file to /etc/ansible/roles/ .
- Update the configuration file to include the Private IP of elk to the elasticSearch and Kibana sections.
- Create a new ansible-playbook filebeat-playbook.yml in the /etc/ansible/roles/ directory that will install, drop in the filebeat.yml and metricbeat.yml files from the /etc/ansible/roles/files/ directory, update the configuration files, and start the service for both Filebeat and Metricbeat.
- Run the playbook, and navigate elk to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- The play book files are metric-playbook.yml, and filebeat-playbook.yml, and the should be moved to the /etc/ansible/roles
- you need to update the filebeat-config.yml and metric-config.yml which are dopped in during the playbook, add the IP on lines 1106 and 1806. when you update the .cfg you will specify a new [elk] group and the ip address associated with it.
- to make sure the platform is running http://52.250.19.130:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
-  ssh -i /c/Users/mboli/id_rsa_azure redAdmin@104.42.115.44
- sudo docker container list -a (locates ansible container, use latest)
- sudo docker start magical dirac (this starts container name)
- sudo docker attach magical dirac (this attaches the container)
- eval $(ssh-agent) && ssh-add /root/newkey (this allows the public key to be used)
- ansible all -m ping (this makes sure ansible is able to connect)
- ansible-playbook /etc/ansible/roles/install-elk.yml (uses the install elk playbook)
- ansible-playbook /etc/ansible/roles/filebeat-playbook.yml (uses the filebeat playbook)
- ansible-playbook /etc/ansible/roles/metric-playbook.yml (uses the metricbeat playbook)
- open a web browser http://52.25.19.130:5601/app/kibana#/home (this takes you to the kibana web portal)
