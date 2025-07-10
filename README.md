<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Melvin J Bonner  
**Email:** melvinj.bonner@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is an isolated section of the AWS cloud where you can launch AWS resources in a virtual network that you define.

### How I used Amazon VPC in this project

In this project I used Amazon VPC to demonstrate how peering works.  

### One thing I didn't expect in this project was...

One thing I didn't expect is how well EC2 Instance Connect worked. I expected to run into some of the same issues I ran into using VS Code.

### This project took me...

The project too me 3 hours. 

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will be creating two VPCs using the VPC wizard. 

### Step 2 - Create a Peering Connection

In this step I will be bridging the two VPCs together with a peering connection.  

### Step 3 - Update Route Tables

In this step, I will be connecting the incoming and outgoing traffic between VPC 1 and VPC 2.

### Step 4 - Launch EC2 Instances

In this step, I will be launching an EC2 instance in each VPC, in order to test the peering connection between my two VPCs.   

---

## Multi-VPC Architecture

I started my project by launching two VPCs. I created 1 subnet for each VPC. 

The CIDR blocks for VPC1 and VPC 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique IPv4 CIDR blocks so the IP addresses of their resources don't overlap. Having overlapping IP addresses could cause routing conflicts and connectivity issues.

### I also launched 2 EC2 instances

I didn't set up key pairs for these EC2 instances as AWS will manage the key pairs for me using EC2 Instance Connect.

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a direct connection between two VPCs. 

VPCs would use peering connections to route traffic between them using their private IP addresses. This means data can now be transferred between VPCs without going through the public internet.

In a peering connection the requester is the VPC that initiates a peering connection. The requester sends the other VPC an invitation to connect. The accepter is the VPC that receives a peering connection request and the accepter can either accept or decline the invitation. 

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs' route tables needs to be updated because the traffic in VPC 1 won't know how to get to the resources in VPC 2 without a route in my route table. I needed to set up a route that directed traffic bound for VPC 2 to the peering connection I set up.

My VPCs' new routes have a destination of 10.1.0.0/16 and 10.2.0.0/16. The routes' target was the peering connection.  

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will be using EC2 Instance Connect to connect to my first EC2 instance.

### Step 6 - Connect to EC2 Instance 1

In this next step, I will be connecting to the EC2 instance with Instance Connect.  

### Step 7 - Test VPC Peering

In this next step, I will try to connect instance 1 to instance 2. I will be sending messages from to instance 2 and have instance 2 send messages back.  

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to connect to my first EC2 instance.

I was stopped from using EC2 Instance Connect originally, because there was no public IPv4 address assigned to the EC2 instance.  

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up an Elastic IP address. The IP addresses are static, meaning that they remain the same even after the EC2 is restarted.

Associating an Elastic IP address resolved the error because the EC2 is now assisgned a public IPv4 address. 

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the ping command from EC2 1 to EC2 2.

A successful ping test would validate my EC2 peering connection because it shows replies from the ping message I sent. Traffic is successfully reaching EC2 instance 2.

I had to update my second EC2 instance's security group because ICMP traffic was being blocked and ping messages are ICMP traffic.  I added a new rule that allowed ICMP traffic.

![Image](http://learn.nextwork.org/zealous_maroon_serene_raspberry/uploads/aws-networks-peering_7a29d352)

---
