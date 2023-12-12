# Creating a Virtual Machine
- [Creating a Virtual Machine](#creating-a-virtual-machine)
  - [Login:](#login)
  - [Creating an Instance of EC2:](#creating-an-instance-of-ec2)
  - [Configuring a new EC2:](#configuring-a-new-ec2)


## Login:
* Head to the AWS console login
* Enter your given AWS credentials along with organisation name
* Go to the Search bar and look for 'EC2' to go the appropriate VM tab

![Alt text](EC2SearchScreenshot.PNG)
  
## Creating an Instance of EC2:
* Click on the Instance tab to see all running VMs
* Filters can be applied to look for local Virtual Machines
* Click 'Launch Instance' to create a new instance

## Configuring a new EC2:
* Names are typically in the format organisation-name-description
    * i.e. tech242-affiq-test-vm
* Select the appropriate Image to launch from (AMI)
    * Typically we use </br>
     ```
     ubuntu/images/hvm-ssd/ubuntu-bionic-18.04-amd64-server-20230424 ami-0a7493ba2bc35c1e9
     can be located by filtering for 20230424
     ```
![Alt text](UbuntuAMI.PNG)

* Choose the correct instance type
    * To minimise costs, choose instance types with the AWS free tier tag
* Choose the correct key pair value, these can be self managed by yourself, in which case you must generate your own .pem credentials, or managed by your organisation who are responsible for sending you a .pem file
* Choose to create a new or an existing security groups - these manage some traffic rules to your system
    * When creating a new group, ensure to allow SSH traffic from only your IP
    * Checkboxes allow multiple selects, so you can enable HTTP requests to the VM
    * You can further click the Edit options for more configurations, such as giving meaningful names
* Review changes in summary section on right-hand side
* Click Launch Instance

After the creation of a new instance, the VM should start running automatically.

![Alt text](IdealSecGroupConfig.PNG)

