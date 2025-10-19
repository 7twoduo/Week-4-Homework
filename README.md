Working with VPC

In the Images, I have created a VPC with amazon web services, took a picture of my highest score of cisco binary game, took a screenshot of steven Marrek SAA course, and the network architecture.
created a private and public subnet from which I jumped into the private subnet via a bastion host through ssh and using a .pem file to get it. 

I did the RDP method, The instances inside the private subnet cannot run httpd servers because they have no access to the internet but i can ssh and icmp them to confirm they exist and i can interact with them.
Nice trick the writer of this weeks homework.

Making an RDP server that can connect to ec2 instances in 3 different private subnets in 3 different availability Zones
Start by making a new VPC and assigning at least 3 private and public ip address subnets withing the maximum CIDR range of 0/16 in aws.
Make 2 security groups, the first one should have RDP enabled on all ipv4 addresses and the second one should have icmp,and ssh on it. The icmp should be configured to the first security group.
Create the RDP instance for the first security group, make sure when creating it to set it up in the right VPC and in a public subnet. Create a private key which you will use for all these instances for the sake of speed and assign it to this instance(make sure to download it). Set the RDP security group to this instance, launch it after.
Create 3 different instances in 3 different private availability zones within this vpc and set the right security group, assign the same private key and launch it.
Now connect to the RDP instance through Windows or Mac(download Windows App), go to the connect button on aws and click and then go to the RDP selection, download the thing you need inorder to connnect to your instance in the public subnet, then click create password and input the private key that you downloaded when making all trhe instnaces.
It will spit out a password and after you run the thing you downloaded for windows or linux, it will require a passowrd and this newly created password is what you will use to RPD into your instances in the private subnet.
Now to confirm the existance of all the other instances, ping all of them through the CLI on your new RPD connection, using the ping (private-ip) to see if your instance has connectivity to these other instances and to check if they exist. Next is to create a .pem file to use to ssh into all 3 instances. Since this is powershell of windows,
this is a little bit more complex so what we need to do is to use the command new-item 'nameitwhatyoulike'.pem, make sure to add the .pem to the file or else it will not work. Next you type the command ssh ec2-user@(private-ip) -i (the.pem file name), and this will allow you to connect to the instance, do this for all the other 3 instances and you will connect.


Tear Down Instructions
Terminate all your instances
Got to VPCs and select your VPC, then detach the internet gateway
Wait 3minutes for AWS to process everything
Then delete all the subnets along with subnet groups
When that is done, delete the VPC and your Done
