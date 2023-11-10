# Configuring-and-deploying-a-highly-available-and-secure-website-by-using-Amazon-Web-Services-AWS-
In this project, I have implemented a highly available website using S3, VPC, EC2, Auto scaling and loan balancers.

configure security for your AWS environment

1. Create a network ACL named WebServer-ACL-34050923 that uses the Lab VPC A VPC in the US East (Ohio) region.

2. Add four inbound rules to the WebServer-ACL-34050923 ACL by using the values in the following table. For any property that is not specified, use the default value.

100	HTTP (80)	80
200	HTTPS (443)	443
300	All ICMP - IPv4	ALL
400	Custom TCP	32768-65535

3. Add an outbound rule that allows all traffic, and then configure a rule number of 100.

4. Associate all available subnets to the WebServer-ACL-34050923 ACL.

5. Create a security group by using the values in the following table. For any property that is not specified, use the default value.

Security group name -	WebServer-SG-34050923

Description-	Security group for HTTP access

VPC-	Lab VPC A

Inbound rule 1-	Type: HTTP Source type: Anywhere-IPv4

Inbound rule 2	Type: HTTPS Source type: Anywhere-IPv4

Inbound rule 3	Type: All ICMP - IPv4cSource type: Anywhere-IPv4

Create a multi-region Amazon S3 bucket for public assets

6. Create a new Amazon S3 bucket named web-bucket-34050923-1 in the US East (Ohio) region, and then enable bucket versioning for the bucket.

7. Create a new S3 bucket named web-bucket-34050923-2 in the US West (Oregon) region, and then enable bucket versioning for the bucket.

Configure a new replication rule named EastWestCRR for all objects in the web-bucket-34050923-1 bucket that uses the existing S3ReplicationRole-34050923 IAM role, and then enable cross-region replication (CRR) to web-bucket-34050923-2.

8. Create a document named welcome.txt, and then add Hello challenge user! to the document.

9. Upload the document to web-bucket-34050923-1, and then verify that the document replicates to web-bucket-34050923-2.

10. Open image.jpg, and then save it on your local computer.

11. Switch to the web-bucket-34050923-1 bucket, and then upload the image.jpg file.

12. Enable public access for web-bucket-34050923-1 and web-bucket-34050923-2.

13. Configure object ownership to enable access control lists (ACLs) in web-bucket-34050923-1.

14. Make the welcome.txt and image.jpg objects in web-bucket-34050923-1 public using ACLs.

15. Create a new IAM user named devone-34050923, configure AWS Management Console access by using LabPassw0rd! as the password, do not require a password reset, and then set a permissions boundary by using the LabSecureAccess policy.

16. Create a new IAM policy named devuserspolicy-34050923 that provides all S3 permissions to the web-bucket-34050923-1 bucket.

17. Create an IAM group named devusers-34050923, and then assign the devuserspolicy-34050923 policy to the group.

18. Add the devone-34050923 user to the group.

19. Create an empty target group named WebServerTG-34050923 in Lab VPC A in the US East (Ohio) region.

20. Create an Application Load Balancer in the US East (Ohio) region by using the values in the following table. For any property that is not specified, use the default value.

Load balancer type	-Application Load Balancer

Name-	WebServerALB-34050923

VPC	-Lab VPC A

Availability Zones- us-east-2a and us-east-2b

Security Group-	WebServer-SG-34050923

Target group-	WebServerTG-34050923

21. Create an Auto Scaling group by using the values in the following table. For any property that is not specified, use the default value.

Auto Scaling group name	WebServerASG-34050923

Launch template	WebServerLT-34050923

VPC-	Lab VPC A

Subnets-	Public Subnet A1 and Public Subnet A2

Enable load balancing	Attach to an existing load balancer

Target group-	WebServerTG-34050923

Desired capacity-	2
Minimum capacity-	2
Maximum capacity-	4

Scaling policies-	Target tracking scaling policy
Target value-	80

Tag Key-	Name

Tag Value-	Web Server

22. Test the new website by using the Application Load Balancer

23. Record the DNS name of the WebServerALB-34050923 load balancer:
    
Go to <ALBDNSName>, and then monitor the change in instance when you refresh the browser.
