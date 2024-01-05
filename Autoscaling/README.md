# Autoscaling Groups


### Create a VM and an AMI
We will need to successfully try and create our target application inside a VM using an AMI and App Data. It is important to follow the normal process of testing the application at each automation stage, and so we will obtain:
* An AMI used to create our application
* App Data used to launch our application

## Creating a Launch Template
Navigate to ```EC2 > Launch Templates``` and click the ```Create Launch Template``` button.

Follow the same rules as you would do to create an instance from an AMI. Namely we will need to fill out:
* Name
* Our AMI
* Our Instance Type
* Our Key-Pair value
* Our security group
* Our resource tag
* Our user data

We can **ignore**:
* Template version description
* Subnet (will be determined by ASG.)

![Alt text](CreateLaunchTemplate1.PNG)
![Alt text](CreateLaunchTemplate2.PNG)
![Alt text](CreateLaunchTemplate3.PNG)
![Alt text](CreateLaunchTemplate4.PNG)
![Alt text](CreateLaunchTemplate5.PNG)
![Alt text](CreateLaunchTemplate6.PNG)

## Testing our Launch Template
To test whether or not our Launch Template has the right configurations, checkbox the template to test and then under ```EC2 > Launch Templates``` and click the button ```Actions > Launch instance from template```.

![Alt text](LaunchInstanceFromTemplate.PNG)

Then you would run an arbritary method do check the deployment of an instance (in our case we would check the public ip and see if the website is running.)

## Creating an Autoscaling Group
We will create an Autoscaling Group by navigating to ```Auto scaling > Auto scaling groups``` and click Create Auto scaling Group.

![Alt text](CreateASG1.PNG)
![Alt text](CreateASG2.PNG)
![Alt text](CreateASG3.PNG)
![Alt text](CreateASG4.PNG)
![Alt text](CreateASG4b.PNG)
![Alt text](CreateASG6.PNG)
![Alt text](CreateASG7.PNG)
![Alt text](CreateASG8.PNG)
![Alt text](CreateASG9.PNG)

## Testing ASG Through Load Balancer
We will then need to navigate to our specific load balancer by finding it under ```Load Balancing > Load Balancer``` and filtering for our LB. Once selected, copy the ```DNS Name```.

![Alt text](TestLB.PNG)