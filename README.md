# How this AWS online shop is built

This project runs a shopping website on AWS. Customers reach it through layers of protection, and the database sits in a hidden area nobody on the internet can touch. Tap any block below to see what it is, why it is used, and where it sits.

**WAF = security guard**Blocks bad visitors at the gate

**Load balancer = reception**Sends each visitor to a free desk

**Private servers = back office**Do the work, closed to the public

**RDS = vault**Keeps customer and order data safe

**0%**

0 of 37 steps

## Architecture map

Read it top to bottom: a customer’s request travels down through each layer. Orange is public, teal is private, purple is security, blue is monitoring.

## Deployment roadmap

The 37 steps in README order, each with a plain explanation. Tick steps as you finish them. Your ticks are saved in this browser.



AWS Production Smart eCommerce Platform
Complete Step-by-Step Deployment Roadmap — Amazon Linux
Purpose: This document is a practical deployment runbook. Follow the sections in order.

Important: Replace every value marked REPLACE_ME, YOUR_*, <...>, or example.com with your own value before running the command.

Operating System: Amazon Linux only. Ubuntu commands such as apt are intentionally not used.

Architecture: 8 subnets, CloudFront, Route 53, WAF, ACM, ALB, ASG, Launch Template + app-server AMI, Nginx, private frontend/backend, RDS, Prometheus, Grafana, PagerDuty, CloudWatch, Lambda, S3, SSM, NAT Gateway, VPC Endpoints, Secrets Manager, and a controlled public monitoring proxy.

How this AWS online shop is built
This project runs a shopping website on AWS. Customers reach it through layers of protection, and the database sits in a hidden area nobody on the internet can touch. Tap any block below to see what it is, why it is used, and where it sits.

WAF = security guard
Blocks bad visitors at the gate
Load balancer = reception
Sends each visitor to a free desk
Private servers = back office
Do the work, closed to the public
RDS = vault
Keeps customer and order data safe
100%
37 of 37 steps
All steps complete. Your platform is deployed and validated.
Architecture map
Read it top to bottom: a customer’s request travels down through each layer. Orange is public, teal is private, purple is security, blue is monitoring.

Outside AWS
The public internet

Customer’s browser
↓
AWS edge, worldwide
First stop for every visitor. Protects and speeds up the site.

Route 53
CloudFront
WAF
ACM
↓
Public subnets (inside your VPC)
The only part of your own network that faces the internet.

Load Balancer (ALB)
NAT Gateway
Monitoring proxy
↓
Private subnets: frontend
Servers that show the website. Not reachable directly from the internet.

Nginx and frontend servers
Auto Scaling Group
↓
Private subnets: backend
Servers that run the shop’s logic and talk to the database.

Flask and Gunicorn backend
↓
Private subnets: database
The most protected area. Only the backend may enter.

RDS database
Security and access, applies to everything
Rules, secrets and admin access that wrap around all the layers.

VPC, subnets and routes
IAM roles
Security Groups
Secrets Manager
VPC Endpoints
Systems Manager (SSM)
Monitoring and logging
Watches the system and keeps records so you can spot problems.

Datadog
CloudWatch
Lambda
S3 log bucket
Prometheus, Grafana, PagerDuty
Load Balancer (ALB)
Public
What it is
Receives traffic and spreads it across healthy servers.
Why it is used here
It is the only door into your private servers, and it removes broken servers from rotation.
Where it sits
Public subnets (inside your VPC)
Built in roadmap steps
Step 20
Step 21
Step 23
Deployment roadmap
The 37 steps in README order, each with a plain explanation. Tick steps as you finish them. Your ticks are saved in this browser.

Workstation and access
2 of 2
Get your account and computer ready.

1
Prepare AWS account and local workstation
Create the account, turn on MFA and install tools.

2
Configure AWS CLI profiles
Let your terminal talk to AWS safely.
Network foundation
6 of 6
Build the private network everything lives in.
Security and data
4 of 4
Set permissions, firewalls and the database.
Application servers
11 of 11
Run the app and make it scale.
Edge and DNS
4 of 4
Put the protected front door on the site.
Monitoring and logging
6 of 6
Watch the system and keep records.
Testing and validation
4 of 4
Prove it all works and is secure.


1. ARCHITECTURE OF 3-TIRE  E-COMMERCE APPLICATION.

                            INTERNET
                               │
                               ▼
                            Route 53
                               │
                               ▼
                           CloudFront
                               │
                               ▼
                              WAF
                               │
                               ▼
                   Application Load Balancer
                           HTTPS :443
                               │
                +--------------+--------------+
                |                             |
                v                             v
       Frontend-Private-1             Frontend-Private-2
                |                             |
                +--------------+--------------+
                               |
                       Nginx Reverse Proxy
                               |
                +--------------+--------------+
                |                             |
                v                             v
         Backend-Private-1             Backend-Private-2
                |                             |
                +--------------+--------------+
                               |
                               v
                              RDS
                        DB Private-1 / 2


                MONITORING ACCESS
                       |
                   Developer
                       |
                       v
              Public Proxy Server
                       |
                     Nginx
                +------+------+
                       |
                Install Datadog
                    |
                LOGGING
                   |
           CloudWatch / Sources
                   |
                Lambda
                   |
                   v
                  S3


              ADMINISTRATION
                   |
                  SSM
                   |
    +--------------+---------------+
    |              |               |
 Frontend       Backend        Monitoring
  Servers        Servers        Servers



---

# 1. Deployment Roadmap

Follow this order:

```text
01. Prepare AWS account and local workstation
02. Configure AWS CLI profiles
03. Create VPC
04. Create 8 subnets
05. Create Internet Gateway
06. Create NAT Gateways
07. Create route tables
08. Create VPC endpoints
09. Create IAM roles
10. Create Security Groups
11. Create RDS
12. Configure Secrets Manager
13. Create backend server
14. Connect backend to RDS
15. Install Flask/Gunicorn
16. Install and configure Nginx
17. Create frontend server
18. Create app-server AMI
19. Create Launch Template
20. Create Target Group
21. Create ALB
22. Create ASG
23. Configure health checks and scaling
24. Create CloudFront
25. Configure ACM
26. Configure Route 53
27. Configure WAF
28. Install Datadog
29. Configure monitoring reverse prox
30. Configure CloudWatch
31. Configure Lambda logging
32.  Create S3 log bucket
33. Configure SSM
34. Test complete application
35. Test monitoring
36.  Test logging
37. Perform security validation
