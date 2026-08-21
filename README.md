# AWS-LOAD-BALANCER

### NAME: B. Khaja Rasool
### REG NO: 212224230040

## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
## Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

## Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

## Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

## Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

## Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

## Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## COMMANDS
No CLI commands are used in this experiment, as it is performed entirely through the AWS Management Console (GUI-based setup) using EC2, Elastic Load Balancing, Auto Scaling, and CloudWatch services.

## OUTPUT
<img width="1920" height="1080" alt="Screenshot (481)" src="https://github.com/user-attachments/assets/9127f571-6d16-4c99-a675-047525587278" />
<img width="1920" height="1080" alt="Screenshot (480)" src="https://github.com/user-attachments/assets/5d074b5f-e938-4c8b-b9bf-e5cb4b56864a" />
<img width="1920" height="1080" alt="Screenshot (484)" src="https://github.com/user-attachments/assets/4e2283a7-ebc0-4012-9a9a-12bdf688fc50" />
<img width="1920" height="1080" alt="Screenshot (489)" src="https://github.com/user-attachments/assets/5d1f01d6-332f-4c08-b2e4-a1ca5e765a1f" />
<img width="1920" height="1080" alt="Screenshot (487)" src="https://github.com/user-attachments/assets/3f17f4f8-c78b-4d33-bf33-20fe2e781534" />
<img width="1920" height="1080" alt="Screenshot (490)" src="https://github.com/user-attachments/assets/0fe753ba-96fc-4642-8762-021531069a79" />







## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.









