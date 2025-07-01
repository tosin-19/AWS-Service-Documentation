# Elastic Compute Cloud [EC2]
Amazon EC2 (Elastic Compute Cloud) is a web service from AWS that provides resizable virtual servers, called instances, in the cloud. These servers allow you to run applications without owning physical hardware.

🔹 Key Concepts
Term	Description
Instance	A virtual server in EC2 used to run applications.
AMI (Amazon Machine Image)	A template containing the OS, application server, and applications.
Instance Type	Defines the hardware (CPU, memory, storage) for the instance. E.g., t2.micro, m5.large.
EBS (Elastic Block Store)	Persistent block storage volumes for EC2.
Key Pair	Used for SSH access (public/private key).
Security Group	Acts like a virtual firewall, controlling inbound/outbound traffic.
Elastic IP	Static public IPv4 address that you can allocate to an instance.
User Data	Script or commands that run when an instance starts (used for bootstrapping).

🔹 EC2 Lifecycle
Launch instance (select AMI, instance type, security group)

Configure networking and storage

Connect using SSH (Linux) or RDP (Windows)

Monitor and manage with CloudWatch

Terminate or stop/start as needed
Launching an EC2 Instance (Steps)
Choose an AMI
Example: Amazon Linux 2, Ubuntu, Microsoft Windows Server

Choose an Instance Type

Example: t2.micro (1 vCPU, 1 GiB RAM – Free Tier eligible)

Configure Instance Details

Number of instances

IAM role

Shutdown behavior

User data (startup script)

Add Storage

Default: 8 GiB (general purpose SSD)

Configure Security Group

Allow SSH (port 22) or RDP (port 3389)

Create/Select Key Pair

.pem file used to connect via SSH

Launch

🔹 Connecting to EC2
Linux (SSH):
bash
Copy
Edit
chmod 400 my-key.pem
ssh -i "my-key.pem" ec2-user@<Public-IP>
Windows (RDP):
Use key pair to decrypt Administrator password

Connect via Remote Desktop using IP and credentials

🔹 EC2 Instance Types (Families)
Family	Use Case
t	General purpose (e.g. t3.micro)
m	Balanced compute/memory (e.g. m5.large)
c	Compute-optimized (e.g. c6g.large)
r	Memory-optimized (e.g. r5.large)
g	GPU workloads (e.g. g4dn.xlarge)
h/i/d	Storage optimized
🔹 Elastic Block Store (EBS)
Attached to EC2 like a virtual disk

Types:

gp3 (General Purpose SSD – default)

io2 (Provisioned IOPS SSD)

sc1/st1 (Cold/Throughput HDD for low-cost storage)

Snapshots: backup of EBS volumes to S3

🔹 Security Groups
Acts like a firewall

Rules allow traffic only (no deny)

Stateless → need to open inbound and outbound rules

Example rule: Allow SSH from your IP → Port 22, Source: your.ip.address/32

🔹 Monitoring & Logging
Amazon CloudWatch monitors:

CPU utilization

Disk I/O

Network traffic

Can set alarms and auto-recovery actions

🔹 Auto Scaling & Load Balancing
Auto Scaling: Automatically adds/removes instances based on demand

Elastic Load Balancer (ELB): Distributes traffic across multiple EC2 instances

🔹 Pricing Models
Model	Description
On-Demand	Pay by the second. No commitment.
Reserved	1- or 3-year commitment with savings.
Spot Instances	Up to 90% discount, can be terminated anytime.
Savings Plans	Flexible pricing model for consistent usage.

🔹 Common Use Cases
Web and mobile app hosting

Batch processing and analytics

Game server hosting

Machine learning model training

Development and testing environments

🔹 Best Practices
Use IAM roles instead of storing AWS credentials on the instance

Restrict SSH/RDP access in security groups

Use EC2 Auto Recovery for fault tolerance

Regularly take EBS snapshots

Enable CloudWatch alarms for resource usage
