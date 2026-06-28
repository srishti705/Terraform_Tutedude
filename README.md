 TuteDude - Terraform Assignment



Deploy Both Flask Backend and Express Frontend on Single EC2 Instances Using Terraform




Provisioning Ec2 instance


Created instance via Terraform










Part 2: Deploy Flask and Express on Separate EC2 Instances


Defing the f




Applying terraform init -upgrade . 



Now , Terrafirm initialised.




Deploy Flask Backend and Express Frontend on Separate EC2 Instances Using Terraform
Project Objective
The objective of this project is to deploy a Flask backend application and an Express frontend application on two separate Amazon EC2 instances using Terraform Infrastructure as Code (IaC).
The infrastructure is designed to automate provisioning, networking, security configuration, and application deployment.

Architecture Overview
The solution provisions:
One EC2 instance for hosting the Flask backend application.
One EC2 instance for hosting the Express frontend application.
A dedicated Virtual Private Cloud (VPC).
Public subnet configuration for internet accessibility.
Security groups to control inbound and outbound traffic.
Automated application installation and startup using user data scripts.

Infrastructure Components
Compute
Two Amazon EC2 instances are created:
Flask Backend Server
Express Frontend Server


Running terraform -upgrade






Running terraform Plan 👍


Networking
Virtual Private Cloud (VPC)
Public Subnet
Internet Gateway
Route Table and Associations
Security
Security groups are configured to:
Allow SSH access for administration.
Allow public access to Flask application port.
Allow public access to Express application port.
Enable communication between application instances.
Automation
User data scripts are used to:
Install required runtime environments.
Configure dependencies.
Start application services automatically during instance initialization.

Deployment Process
Configure Terraform variables.
Initialize Terraform environment.
Validate configuration.
Generate execution plan.
Apply infrastructure changes.
Wait for EC2 provisioning and application startup.
Access applications using public instance endpoints.



Expected Outcome
After successful deployment:
Flask backend runs successfully on a dedicated EC2 instance.
Express frontend runs successfully on a separate EC2 instance.
Both applications are accessible publicly.
Infrastructure is fully managed through Terraform.


Deliverables
Terraform configuration files
Two deployed EC2 instances
Configured networking resources
Security groups with required access rules
Automated deployment through user data scripts
Run : terraform apply to apply changes 




Conclusion
This project demonstrates Infrastructure as Code practices using Terraform to deploy multi-instance applications in AWS. The implementation provides automated provisioning, simplified management, and scalable deployment architecture.
Flask and Express Deployment Using Docker, Terraform, and AWS
Project Overview
This project demonstrates deployment of a Flask backend and an Express frontend as Docker containers using AWS services and Terraform Infrastructure as Code (IaC).
The infrastructure provisions container repositories, networking resources, container orchestration services, and load balancing to provide an automated and scalable deployment environment.

Objectives


Store container images in Amazon Elastic Container Registry (ECR).
Use Amazon ECS to manage container execution.
Configure networking using Amazon VPC.
Route traffic using an Application Load Balancer (ALB).
Manage infrastructure through Terraform.

Services Used
Amazon ECR
Used for storing Docker container images.
Repositories created:
Flask Backend Repository
Express Frontend Repository
Amazon VPC
Provides isolated networking resources.

 

Flask Dockerfile creation via Terraform
Building image for from Dockerfile express : 


Deploy Flask backend as a Docker container.
Deploy Express frontend as a Docker container.
Cross verify ECR  Repository.
Two repository will be there frontend and backend in console created via Terraform code.
Cross verifying Docker images inDocker Desktop : 


Authenticating ECR Repository using below command : 
aws ecr get-login-password --region ap-south-1 | \
docker login --username AWS --password-stdin <ACCOUNT_ID>.dkr.ecr.ap-south-1.amazonaws.com


Step 4 — Tag image
Flask:
docker tag flask-backend:latest \
121710558372.dkr.ecr.ap-south-1.amazonaws.com/flask-backend:latest
Express:
docker tag express-frontend:latest\121710558372.dkr.ecr.ap-south-1.amazonaws.com/express-frontend:latest

Once login:
Push both images to ECR Repository

Adding data.tf , networking.tf and alb.tf  






Components:
VPC
Subnets
Internet Gateway
Route Tables
Security Groups

Amazon ECS
Used to run containerized applications.
Components:
ECS Cluster
ECS Task Definitions
ECS Services
Application Load Balancer (ALB)
Routes incoming requests to ECS services.

Solution Architecture
User Request
↓
Application Load Balancer
↓
ECS Cluster
↓
Flask Backend Container
Express Frontend Container
↓
Docker Images Stored in ECR

Deployment Workflow
Step 1: Container Preparation
Build Docker images for:
Flask backend
Express frontend
Step 2: Push Images to ECR
Authenticate with ECR and upload Docker images.
Step 3: Provision Infrastructure
Terraform provisions:
ECR repositories
VPC and networking
ECS cluster
ECS services
Application Load Balancer
Step 4: Deploy Containers
ECS pulls images from ECR and starts application containers.
Step 5: Validation
Verify:
ECS services are healthy
Containers are running
ALB endpoint is accessible

Terraform Configuration Structure
Recommended structure:
project/
├── provider.tf
├── variables.tf
├── outputs.tf
├── backend.tf
├── vpc.tf
├── ecr.tf
├── ecs.tf
├── alb.tf
├── terraform.tfvars
└── README.md



State Management
Terraform remote state should be configured using S3.
Benefits:
Shared infrastructure state
Better collaboration
Improved reliability
Centralized state storage

Expected Deliverables
Terraform configuration files
Docker images pushed to ECR
ECS cluster deployed
Flask backend service running
Express frontend service running
Application Load Balancer configured
Infrastructure managed through Terraform

Validation Commands
Execute the deployment process using:
Initialize Terraform
Validate Terraform configuration
Review execution plan
Apply infrastructure changes
After deployment, verify application accessibility through the Application Load Balancer endpoint.

Outcome
Upon successful completion:
Flask backend is deployed as a Docker container.
Express frontend is deployed as a Docker container.
Applications are accessible through ALB.
Infrastructure provisioning is fully automated.

Conclusion
This project demonstrates modern cloud deployment practices by combining Docker containerization, Terraform automation, and AWS managed services. The solution provides scalability, automation, maintainability, and simplified infrastructure management.







