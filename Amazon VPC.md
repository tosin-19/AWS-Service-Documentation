# Amazon Virtual Private Cloud
> Amazon Virtual Private Cloud (VPC) is a service that allows you to launch AWS resources, such as EC2 instances, in a logically isolated virtual network that you define. You have full control over your network configuration, including IP address ranges, subnets, route tables, and network gateways.

## Key Features
Full network customization
Private subnets and public subnets
Security groups and network ACLs
Internet gateway, NAT gateway, VPC peering
Flow logs for traffic monitoring
IPv4 and IPv6 support

## Core Components of a VPC
| Component | Description |
| --------- | ----------- |
| VPC |	A logically isolated section of the AWS Cloud |
| Subnets | Subdivisions within a VPC. Can be public or private |
|Route Tables | Determine how traffic is directed |
| Internet Gateway (IGW) | Enables access to the internet for resources in public subnets |
| NAT Gateway | Allows private subnet instances to access the internet securely |
| Elastic IP (EIP) | A static public IPv4 address for dynamic cloud computing |
| Security Groups  | Stateful firewalls attached to instances |
| Network ACLs (NACLs) | Stateless firewall at the subnet level |
| DHCP Options | Sets	Custom configuration for DHCP in your VPC |
| VPC Peering | Connects two VPCs privately |
| VPC Endpoints | Enables private connections to AWS services |
| Flow Logs	| Captures information about IP traffic going to and from network interfaces |

## Subnets
Public Subnet: Associated with a route table that has a route to an Internet Gateway.
Private Subnet: No route to the Internet Gateway (can access the internet via NAT).

## Internet Access in VPC
To allow internet access to an instance:
It must be in a public subnet
It must have a public IP or Elastic IP
The subnet must be associated with a route table pointing to an IGW

## Security Mechanisms
Security Feature	Description
Security Groups	Instance-level security; stateful
Network ACLs	Subnet-level security; stateless

## IP Addressing
Choose your own IPv4 CIDR block (e.g., 10.0.0.0/16)
AWS reserves 5 IPs per subnet
Supports IPv6 for internet-scale applications

## VPC Peering and Endpoints
Peering: One-to-one network connection between two VPCs
Endpoints: Secure, private access to AWS services from within your VPC

## Common VPC Configurations
Simple Public Web App:
1 Public Subnet
Internet Gateway
EC2 with Security Group

Web + App + DB (Multi-tier):
Public Subnet (web)
Private Subnet (app/db)
NAT Gateway
Security Groups with restricted ports
Private VPC with VPN/Direct Connect: No IGW
Connects on-premises data center to AWS

## VPC Best Practices
Design for availability – Use multiple Availability Zones.
Use private subnets – Protect sensitive resources.
Least privilege – Use minimal open ports and IAM policies.
Enable flow logs – For auditing and troubleshooting.
Separate resources – Use subnets by function (web, app, db).
Tag resources – For better management and cost tracking.

## Integration with Other Services
EC2: Most commonly deployed in a VPC
RDS: Can be placed in private subnets
EKS/ECS: Uses VPC for networking
Lambda: Can run in a VPC for database access
S3/DynamoDB Endpoints: Allow access without traversing the internet

## Monitoring and Troubleshooting
Amazon VPC Flow Logs: Capture and analyze traffic
CloudWatch Logs: Integrated with VPC logs
Reachability Analyzer: Test if resources can connect
VPC Traffic Mirroring: Analyze packet-level data

## Pricing
VPC itself is free
Charges apply for: NAT Gateway usage, VPC Traffic Mirroring, Transit Gateway, PrivateLink endpoints

## Common Use Cases
Host a web application securely
Set up a hybrid cloud with VPN/Direct Connect
Isolate resources in multi-tenant applications
Enable secure connections to AWS services using endpoints
Build multi-tier architectures

## CLI/SDK Commands
Create a VPC (AWS CLI):

Bash
Copy
Edit

aws ec2 create-vpc --cidr-block 10.0.0.0/16

Create a Subnet:

bash
Copy
Edit

aws ec2 create-subnet --vpc-id vpc-abc123 --cidr-block 10.0.1.0/24

Attach Internet Gateway:

bash
Copy
Edit

aws ec2 attach-internet-gateway --vpc-id vpc-abc123 --internet-gateway-id igw-abc123

## Conclusion
Amazon VPC is a powerful foundational service in AWS, offering deep control over your cloud network infrastructure. Whether you're running public web apps, secure private systems, or hybrid networks, VPC allows you to architect scalable and secure environments with precision.

