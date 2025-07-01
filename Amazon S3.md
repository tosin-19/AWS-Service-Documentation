Amazon S3 is an object storage service that lets you store and retrieve any amount of data at any time, from anywhere on the web. It’s used for:

Hosting static websites

Backups and restore

Application data storage

Big data and analytics

🔹 Key Concepts
Term	Description
Bucket	A container for storing objects in S3 (like a root folder).
Object	A file or data stored in S3, along with metadata.
Key	The unique name (full path) of an object in a bucket.
Region	A geographical AWS area where the bucket and its contents are stored.
ACL/Policies	Access control settings to manage who can access a bucket or object.
S3 URL	The web address for accessing an object, e.g., https://bucket-name.s3.amazonaws.com/file.txt
Bucket Creation
Open S3 Console
Click "Create bucket"
Configure: Bucket name (globally unique)
Region (e.g., us-east-1)
ACLs and public access settings
Versioning, encryption, logging (optional)
Click "Create bucket"
Uploading Objects
You can: Upload through Console
Use AWS CLI:
Bash	
Copy
Edit
Aws S3 cp myfile.txt s3://my-bucket/
Use Python (Boto3):
Python
Copy
Edit
Import boto3

s3 = boto3.client('s3')
s3.upload_file('myfile.txt', 'my-bucket', 'myfile.txt')
🔹 Access Control
Method	Description
Bucket Policies	Set rules on who can access bucket and what actions are allowed.
IAM Policies	Control user or role access to S3.
ACL (Access Control List)	Fine-grained access for individual objects (older method).
Public Access Settings	Prevents accidental public access (enabled by default).

🔹 Object URL Structure
Format:
php-template
Copy
Edit
https://<bucket-name>.s3.<region>.amazonaws.com/<key>
Example:

bash
Copy
Edit
https://my-bucket.s3.us-east-1.amazonaws.com/images/logo.png
🔹 S3 Storage Classes
Class	Use Case
Standard	Frequently accessed data
Intelligent-Tiering	Automatically moves data between tiers
Standard-IA	Infrequent access (lower cost, retrieval fee)
Glacier	Archival storage (retrieval in minutes to hours)
Glacier Deep Archive	Lowest-cost, longest retrieval time (12+ hours)

Versioning
Keeps multiple versions of an object.

Protects against accidental deletion or overwrite.

Enable in bucket settings.

 Static Website Hosting
You can host a static website from S3:

Enable static website hosting in bucket settings

Upload HTML/CSS/JS files

Make objects public

Access the site via the S3 website endpoint:

arduino
Copy
Edit
http://my-bucket.s3-website-us-east-1.amazonaws.com
🔹 Lifecycle Management
Automate transitions:

Move files to Glacier after 30 days

Delete objects after a certain period

✅ Set via bucket lifecycle rules

🔹 Logging and Monitoring
Tool	Purpose
Server Access Logging	Logs requests to S3 bucket
CloudTrail	Logs API calls (who did what)
CloudWatch	Monitoring metrics like storage usage, requests

🔹 S3 vs EBS vs EFS
Service	Type	Use Case
S3	Object storage	Unstructured data, media, logs
EBS	Block storage	Attached to EC2 like a hard drive
EFS	File storage	Shared file system for Linux EC2

🔹 Pricing (Key Factors)
Storage size (GB/month)

Number of requests (PUT, GET, DELETE)

Data transfer (out to internet)

Storage class used (Standard, Glacier, etc.)

Free tier: 5 GB of Standard storage for 12 months

🔹 Best Practices
Enable versioning for data protection

Use S3 Encryption (SSE-S3 or SSE-KMS)

Set lifecycle policies to reduce cost

Block public access unless necessary

Use CloudFront to speed up access (CDN)

Use MFA Delete for sensitive buckets

