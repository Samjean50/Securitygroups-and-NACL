## Security-and-NACL
### 1. Project Overview
This project explores the configuration and implications of Security Groups and Network Access Control Lists (NACLs) in a cloud environment. The objective is to understand how inbound and outbound rules affect network traffic and security in AWS.

### 2. Objectives
* Learn how to create and configure Security Groups and NACLs.
* Analyze the effect of different security settings on access control.
* Test security rules by modifying inbound and outbound settings.
* Ensure secure communication between instances while maintaining necessary accessibility.

### 3. Purpose
The purpose of this project is to enhance understanding of cloud security mechanisms by implementing and testing Security Groups and NACLs. This will help in securing cloud applications and ensuring proper network traffic flow.

### 4. Requirements
AWS Account with administrative access.
Basic knowledge of cloud networking and security.
An EC2 instance for testing.
Access to AWS Management Console or AWS CLI.
### 5. Use Case
This project is applicable in scenarios where organizations need to regulate access to cloud-based services while maintaining security. For example, an e-commerce application may require open access to users but restrict unauthorized internal communication.

### 6. Performance Goals
Successfully configure Security Groups and NACLs.
Demonstrate how changes in security rules impact accessibility.
Achieve secure yet functional access to cloud-based applications.
Document troubleshooting steps for resolving security-related issues.

### 7. Project Steps and Commands
#### 7.1. Navigate to the security groups section
![security group](images/1.png)
![security group](images/2.png)

* Click create security group and enter the details
![security group](images/4.png)


* Set your inbound and outbound rules and click create
* ![security group](images/5.png)


#### 7.2. Go to Instance
* Go to your Instance section and click change security groups
* ![security group](images/6.png)

* Select your security group and save
![security group](images/7.png)

* Navigate to the open address of the instance on your web browser
![security group](images/9.png)

#### 7.3 Testing Implications of Security Group Rules

#### 7.4. Remove the Outbound Rule and Save
* Deleting the outbound rule
![security group](images/11.png)
![security group](images/12.png)
![security group](images/13.png)

* Absence of outbound rules still has no effect on traffic from instance to the outside
![security group](images/9.png)

#### 7.5. Remove the Inbound Rule and Save
* Deleting inbound rule
![security group](images/14.png)
![security group](images/15.png)
![security group](images/16.png)


* Attempt to access instance via browser
![security group](images/35.png)

#### 7.6. Allow HTTP on Outbound Rule
* Adding HTTP to outbound rule
![security group](images/18.png)

* No inbound rules present
![security group](images/16.png)

* Attempt to access instance via browser (still no access)
![security group](images/35.png)

#### 7.7 Testing Implications of NACL Rules
* Creating a Network ACL
![security group](images/19.png)
![security group](images/20.png)

* Input the information and select your VPC
![security group](images/21.png)

* Modify inbound rules
![security group](images/22.png)

* Go to the outbound rules
![security group](images/23.png)

* Make changes to the inbound rules and save
![security group](images/24.png)
![security group](images/25.png)


* Go to actions and click on subnet associations
![security group](images/26.png)

* Select the subnet and save
![security group](images/27.png)

* Test access to the instance (still no access due to outbound rules blocking traffic)
![security group](images/35.png)

* Modify outbound rules
![security group](images/28.png)

* Add rule and save
![security group](images/29.png)
![security group](images/30.png)
![security group](images/33.png)

Add the same rule for inbound
![security group](images/31.png)
![security group](images/32.png)

* You should now be able to access your site
![security group](images/9.png)

#### 7.8. Testing Implications of Both NACL and Security Group Rules
* Go to your security group and set the inbound rules
![security group](images/36.png)

* Set your outbound rules in the security group
![security group](images/37.png)

* Go to NACL and set rules for both inbound and outbound

For inbound:
![security group](images/25.png)

For outbound:
![security group](images/29.png)

* Try to access the site, it is still inaccessible
![security group](images/35.png)

### 8. Troubleshooting (Common Issues and Solutions)
#### 8.1. Trying to ensure the server was accessible
**Issue:** Could not get access to the server. Solution:
- Ensure an Internet Gateway is attached.
- Verify route tables include a route to 0.0.0.0/0 via the Internet Gateway.
#### 8.2. Subnet Routing Issues
**Issue:** Private instances are not communicating with public instances. Solution:

- Confirm that the route table for private subnets has a NAT Gateway route.
- Ensure the correct subnet associations are applied.

#### 8.3. Security Group Misconfigurations
**Issue:** The instance is not reachable over the expected ports. Solution:

- Ensure the security group allows inbound traffic on required ports (e.g., 22 for SSH, 80 for HTTP, 443 for HTTPS).
- Check if outbound rules are restricting responses.

#### 8.4. NACL Blocking Traffic
**Issue:** Some traffic is being blocked despite security group settings. Solution:

- Verify that the NACL associated with the subnet allows inbound and outbound traffic for the required ports.
- Ensure there are no DENY rules overriding allow rules.

#### 8.5. Instance Connectivity Issues
**Issue:** The instance is unable to connect to external services. Solution:

- If using a private subnet, ensure there is a NAT Gateway for outbound internet access.
- Check the default route in the route table.
