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

---

## Project Details
This cloud project is designed to:

1. Provide a secure and resilient production environment for hosting web applications.
2. Leverage the benefits of a VPC with public and private subnets to enhance the overall security posture.
3. Implement automatic scaling and high availability using an Auto Scaling group and a load balancer.
4. Ensure that the application servers in the private subnets can still access the internet for necessary functionalities.



## VPC Configuration

The Virtual Private Cloud (VPC) is configured to span two Availability Zones for high availability and fault tolerance. It includes both public and private subnets in each AZ. The public subnets are configured with an Internet Gateway to allow inbound and outbound internet access, hosting the load balancer and NAT gateways. Private subnets, where application servers reside, do not have direct internet access. Instead, they use NAT gateways in the public subnets for outbound internet connectivity. This setup ensures a secure network architecture by isolating critical components while maintaining necessary internet access for updates and external services.

![VPC config](https://github.com/user-attachments/assets/cce0284a-a883-4736-b408-eadee9d67fd7)

---
## Auto Scaling Group Configuration

The Auto Scaling group is configured to manage the application servers deployed in the private subnets. It automatically adjusts the number of EC2 instances based on predefined conditions such as CPU utilization or network traffic. The group spans multiple Availability Zones to ensure high availability and fault tolerance. Launch templates or launch configurations are used to define the instance specifications, including the AMI, instance type, key pair, security groups, and user data for initial setup. Scaling policies are set to automatically increase or decrease the number of instances in response to changing demand, ensuring optimal performance and cost-efficiency.

## Subnet Division: Public vs Private

The VPC is divided into public and private subnets across two Availability Zones:

- **Public Subnets**: These subnets have a route to the Internet Gateway, allowing direct internet access. They host the Application Load Balancer and NAT gateways. The load balancer in the public subnets receives incoming traffic and distributes it to the application servers in the private subnets.

- **Private Subnets**: These subnets do not have a direct route to the internet. They host the application servers, databases, and other backend systems that don't require direct internet access. Outbound internet access for these resources is facilitated through NAT gateways located in the public subnets. This configuration enhances security by isolating critical components from direct internet exposure while still allowing necessary outbound connections for updates and external services.
  
![launch template for Auto scalling group](https://github.com/user-attachments/assets/bc65cdd8-8659-4313-b7e6-7de151c60ff4)
![new auto scalling croup](https://github.com/user-attachments/assets/f87b69cc-9735-4c69-aad0-4c3108aa1f4f)
---

## Bastion Host

The bastion host serves as a secure entry point for accessing resources in private subnets:

- Deployed in a public subnet for direct internet access
- Acts as a jump server for SSH access to EC2 instances in private subnets
- Enhances security by minimizing the attack surface of the infrastructure
- Configured with strict security group rules, allowing inbound SSH only from trusted IP addresses
- Requires SSH key authentication for access
- Regularly updated and patched to maintain security posture

To access EC2 instances in private subnets:
1. SSH into the bastion host using its public IP address
2. From the bastion, SSH into private EC2 instances using their private IP addresses

![bastion host to login to our private subnets](https://github.com/user-attachments/assets/7bfa9062-4e05-4c2c-9f25-d56f90aef95d)
---


## Load Balancer: Traffic Management and High Availability

The **Application Load Balancer (ALB)** is deployed in the **public subnets** to manage incoming traffic, distributing requests to application servers in the **private subnets**.

#### Use Case:
- **Traffic Distribution**: The ALB routes incoming traffic to application servers in private subnets, ensuring balanced loads and improved performance.
  
- **High Availability**: Spread across two Availability Zones, the ALB ensures continuous uptime by rerouting traffic to healthy instances in case of failure.
  
- **Auto Scaling Integration**: The ALB works with Auto Scaling to distribute traffic to new instances as demand increases or decreases.

- **Secure Access**: The ALB acts as the internet-facing entry point, securing the private subnet servers by isolating them from direct internet exposure.

- **SSL Termination**: SSL certificates are managed by the ALB, ensuring secure traffic between clients and the load balancer.

![creating load balance and target gorup for load balance5](https://github.com/user-attachments/assets/635e470f-912d-414f-9b6e-a63f5a329cc7)


--- 


## Application Deployment in Private Subnet and Accessing via Bastion Host 

In this project, the application servers are deployed in the **private subnets** to ensure they are isolated from direct internet access. The **Bastion Host** in the public subnet acts as a secure gateway for managing and accessing these instances.

#### Use Case:
1. **Deploying the Application in the Private Subnet**:
   - The web application is hosted on servers within the private subnets to enhance security and isolation. These servers are only accessible internally within the VPC.
   - Application servers are configured to auto-scale based on demand and are not directly exposed to the internet, ensuring that only authorized traffic reaches them via the load balancer. 

![permission denied so changed permission using CHmod cmnd](https://github.com/user-attachments/assets/2210d089-2126-4371-a31a-c1fd6c44ca40)
![logging into the server and creating an app to run on cloud](https://github.com/user-attachments/assets/2123e20a-2d22-411a-a733-2da9c64ec6c7)


2. **Accessing the Private Subnet via Bastion Host**:
   - A **Bastion Host** (jump box) is deployed in the public subnet, allowing secure SSH access to the application servers in the private subnets.
   - Administrators connect to the Bastion Host using SSH and then securely tunnel into the private subnet servers for maintenance or troubleshooting.
   - This access flow ensures the private subnet remains secure while still providing necessary access for managing the application servers.




![working of the app on the server  7](https://github.com/user-attachments/assets/76eb92c9-a2cc-4dd9-87d0-ea32a3ce1c67)


3. **Accessing the Application via DNS**:
   - The application is accessible to users via the **DNS** of the **Application Load Balancer**.
   - End users interact with the ALB’s DNS, which routes their requests to the application servers in the private subnet, ensuring seamless access without directly exposing the servers.
   - This setup maintains a secure environment while providing external access through the ALB.

---



