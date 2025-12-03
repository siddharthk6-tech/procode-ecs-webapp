# Procode ECS WebApp - Terraform Deployment

This repository contains a **Terraform configuration** to deploy a basic containerized web application on AWS using **ECS Fargate**. The infrastructure includes networking, security, and a load-balanced ECS service running an NGINX container.

---

## Architecture

The infrastructure deployed includes:

1. **VPC and Networking**
   - A single VPC with CIDR `10.0.0.0/16`.
   - Two public subnets for ECS tasks and ALB.
   - Internet Gateway with a public route table.
   - Security Groups restricting access to HTTP (port 80) only from a specific IP address.

2. **ECS Fargate**
   - ECS Cluster to run containerized tasks.
   - ECS Task Definition using NGINX container.
   - ECS Service using Fargate launch type.
   - ALB Target Group with health checks on `/` path.
   - ALB Listener on port 80.

3. **Load Balancer**
   - Application Load Balancer (ALB) in public subnets.
   - ALB security group allows HTTP only from allowed IP.

4. **Terraform Backend**
   - State stored in S3 bucket.
   - DynamoDB table used for state locking.

---

## Prerequisites

- AWS CLI configured with appropriate credentials.
- Terraform installed (v1.3+ recommended).
- An AWS account with permissions to create:
  - VPC, Subnets, Security Groups
  - ECS Cluster, Tasks, Services
  - IAM Roles and Policies
  - Application Load Balancer
  - S3 Bucket and DynamoDB (for remote state)

---

## How to Deploy

1. **Clone the repository**
```bash
git clone https://github.com/siddharthk6-tech/procode-ecs-webapp.git
cd procode-ecs-webapp
```

2. **Initialize Terraform**

```bash
terraform init
```


3. **Review the planned infrastructure**

```bash
terraform plan
```


4. **Apply the configuration**

```bash
terraform apply -auto-approve
```

---

## Outputs

**alb_dns_name** → Access the web application using this ALB DNS.

**ecs_cluster_name** → Name of ECS Cluster.

**ecs_service_name** → Name of ECS Service.

**vpc_id** → VPC ID.

**subnet_ids** → List of public subnet IDs.

**security_group_id** → Security Group ID for ECS tasks.

---

## Testing the Deployment

Visit the alb_dns_name in your browser.

You should see the NGINX welcome page indicating the container is running successfully.






