# Virtual Private Clouds (VPCs)

## In Brief
* VPC is a Virtual Private Cloud
* Inevitably a huge part of the exam. (I would imagine!)
* A logically (but not usually physically) isolated part of the AWS cloud that has internal networking but no internet connectivity by default.
* Building a VPC
* NATs
* Security Groups
* Subnets
* Route Tables
* ACLs
* NAT vs Bastion

## Creating a VPC

* All AWS accounts come with a default VPC that has an internet gateway.
  * Just to make sure people can get started. Not a good place to start for a super-secure application.
* Fully-isolated network. No access to any resources inside it from the internet by default.

* Top-level = VPC (covers multiple AZs, one region)
  * VPC contains multiple subnets (1 subnet = 1 AZ)
    * Subnet has internal CIDR block (10.0.1.0/16, 10.0.2.0/16, etc.)
    * Can be told to assign public IPs to instances inside it by default, or not (default).
  * Subnets can be public or private. (Public if they have a public IP address, although this does not neccessarily guarantee access.)
* VPC is ultimately uncontactable from the web without an internet gateway, even with public subnets.
  * Can you even assign a public IP address to an instance in a public subnet in a VPC with no internet gateway? (Not sure...)

## Security Groups

* 1st-line defence for instances. Assigned to an instance (or group of instances)
* Assumes all inbound traffic for all protocols is blocked by default.
* User grants permission to:
  * CIDR block/another security group/everywhere for
  * Protocol or port range
* By default, all outbound traffic is permitted but this can be deleted and replaced with tighter restrictions.

## Subnets

* Inside an availabilty zone. Assigned private CIDR within VPC.
  * CIDR can't overlap within VPC.
* Often have one VPC and multiple subnets spanning minimum 2 AZs. (Only two AZs in London anyway)
* Can tell instances within a subnet to be assigned public IPs by default or not (making them public or private)

## ACLs (Access Control Lists)

* Second line defence (after security groups)
* Default allow all inbound & outbound.
  * Manually created **blocks all inbound and outbound**
* More fine grained. Attached to... subnet? (Need to check this)
* Works on numbered priority
* Can assign an ACL to multiple Subnets
  * But each subnet can only be assigned to one ACL at a time

## NAT Gateway vs Bastion

Two ways to traverse private subnet -> public subnet -> internet Gateway:

1. Bastion host. Set up instance in public subnet. Use route tables to route traffic through bastion in public subnet.
2. NAT gateway. Does the same thing, but highly available. *(Not necessarily in the exam.)*

**NAT gateways are the right way to do this, however it may not be defined as a solution in the exam.**

## VPNs

* Possible to set up a public subnet containing a VPN server to allow access to a private subnet.
* Again, may not be defined in the exam.
