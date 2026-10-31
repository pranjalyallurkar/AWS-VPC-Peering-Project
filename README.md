# AWS-VPC-Peering-Project
AWS VPC Peering with EC2 instances, private subnets, route tables and security groups.

# AWS VPC Peering Project

## Overview

This project demonstrates how to establish secure communication between two Amazon Virtual Private Clouds (VPCs) using **AWS VPC Peering**.

The architecture uses EC2 instances, public and private subnets, route tables, Internet Gateway, and security groups to enable private communication between resources in two different VPCs.


## 📁 Project Structure (AWS VPC Peering Architecture Diagram)

<p align="center">
  <img width="1536" height="1024"
       alt="AWS VPC Peering Architecture"
       src="https://github.com/user-attachments/assets/8727f438-714a-431a-a1c8-e1297713a7b7" />
</p>

## Project Objectives

- Create two separate VPCs with different CIDR ranges.
- Configure public and private subnets.
- Launch EC2 instances in the respective subnets.
- Configure security groups to control inbound and outbound traffic.
- Establish a VPC Peering connection between VPC A and VPC B.
- Update route tables to enable communication between the VPCs.
- Verify connectivity using SSH and ICMP (Ping).

## AWS Architecture Details

### VPC A – my-vpc

| Component | Configuration |
|---|---|
| VPC CIDR | `10.10.0.0/16` |
| Public Subnet | `10.10.1.0/24` |
| Private Subnet | `10.10.2.0/24` |
| Internet Gateway | `ewb-igw-a` |
| Public Route Table | `ewb-rt-a-public` |
| Private Route Table | `ewb-rt-a-private` |

### VPC B – ewb-vpc-b

| Component | Configuration |
|---|---|
| VPC CIDR | `10.20.0.0/16` |
| Private Subnet | `10.20.1.0/24` |
| Private Route Table | `ewb-rt-b-private` |

## EC2 Instances

| Instance | Subnet | Private IP | Public IP |
|---|---|---|---|
| ewb-bastion | Public Subnet A | `10.10.1.10` | Enabled |
| ewb-app-a | Private Subnet A | `10.10.2.10` | Disabled |
| ewb-app-b | Private Subnet B | `10.20.1.10` | Disabled |

## Technologies Used

- Amazon Web Services (AWS)
- Amazon VPC
- EC2 (Elastic Compute Cloud)
- VPC Peering
- Internet Gateway (IGW)
- Route Tables
- Security Groups
- Amazon Linux 2023
- SSH
- ICMP / Ping

## Implementation Steps

1. Created VPC A and VPC B with separate CIDR blocks.
2. Created public and private subnets.
3. Attached an Internet Gateway to VPC A.
4. Created and configured route tables.
5. Created security groups for Bastion, App-A, and App-B.
6. Created an EC2 key pair for secure SSH access.
7. Launched three EC2 instances in the appropriate subnets.
8. Created a VPC Peering connection between VPC A and VPC B.
9. Accepted the peering request.
10. Updated route tables to enable communication between the VPCs.
11. Tested connectivity between the EC2 instances.

## VPC Peering Configuration

The following routes are required after establishing the peering connection:

| Route Table | Destination | Target |
|---|---|---|
| VPC A Public RT | `10.20.0.0/16` | VPC Peering |
| VPC A Private RT | `10.20.0.0/16` | VPC Peering |
| VPC B Private RT | `10.10.0.0/16` | VPC Peering |

The existing local routes and the public route table's Internet Gateway route must also be retained.

## Security Configuration

Security groups control access to the EC2 instances.

- **Bastion:** SSH access from the administrator's public IP.
- **App-A:** SSH access from the Bastion and ICMP Echo Request from App-B.
- **App-B:** SSH access from the Bastion and ICMP Echo Request from App-A.

Private EC2 instances do not require public IP addresses.

## Connectivity Testing

After configuring VPC Peering and route tables, test connectivity.

From App-A, test App-B:

```bash
ping -c 4 10.20.1.10
```

From App-B, test App-A:

```bash
ping -c 4 10.10.2.10
```

Successful replies indicate that network connectivity is working.

## Expected Outcome

- Two separate VPCs connected through VPC Peering.
- Secure communication between private EC2 instances.
- Private instances accessible through the Bastion host.
- Route tables configured for cross-VPC communication.
- Security groups restricting access to specified sources.

## Learning Outcomes

Through this project, I learned:

- AWS VPC and subnet configuration.
- Public and private networking.
- EC2 instance deployment.
- Security group configuration.
- VPC Peering and routing.
- SSH connectivity and network troubleshooting.

## Project Status

**Status:** In Progress / Completed

Update this status after completing and testing all configurations.

## Author

**Name:** Pranjal Yallurkar

**GitHub:** https://github.com/pranjalyallurkar

---

*This project was created for hands-on learning and practical understanding of AWS networking and VPC Peering.*
