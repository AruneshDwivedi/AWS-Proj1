# Cloud Project with VPC: Secure and Resilient Production Environment

## Overview
This cloud project demonstrates the use of a Virtual Private Cloud (VPC) with both public and private subnets to create a secure and resilient production environment. 
 
   Key aspects of the architecture:
- **VPC Design**: The VPC spans two Availability Zones and consists of public and private subnets.
- **Public Subnets**: These subnets host the load balancer and NAT gateways, providing internet connectivity.
- **Private Subnets**: The application servers are deployed in these subnets, which are not directly accessible from the internet.
- **Auto Scaling**: The application servers are managed by an Auto Scaling group, ensuring high availability and automatic scaling.
- **Load Balancing**: An Application Load Balancer is used to distribute traffic to the application servers.
- **Internet Connectivity**: The application servers in the private subnets can access the internet through the NAT gateways in the public subnets.
 ---
 
![Screenshot 2024-09-20 143054](https://github.com/user-attachments/assets/1be85f95-fc5d-4446-b7f0-178bf056b006)



## Project Details
This cloud project is designed to:

1. Provide a secure and resilient production environment for hosting web applications.
2. Leverage the benefits of a VPC with public and private subnets to enhance the overall security posture.
3. Implement automatic scaling and high availability using an Auto Scaling group and a load balancer.
4. Ensure that the application servers in the private subnets can still access the internet for necessary functionalities.
