# EKS Terraform Module

This module provisions an Amazon EKS (Elastic Kubernetes Service) cluster, managed node groups, and all required IAM roles and policies for a production-ready Kubernetes environment.

## Purpose
- Deploy a secure, scalable EKS cluster
- Automate node group management and scaling
- Enable GitOps and ArgoCD integration

## Features
- EKS cluster with configurable Kubernetes version
- Managed node groups with auto-scaling
- IAM roles for cluster and nodes
- Cluster logging enabled
- Security group for EKS control plane
- Outputs for integration with other modules

## Usage
```hcl
module "eks" {
  source              = "./modules/eks"
  project_prefix      = var.project_prefix
  environment         = var.environment
  aws_region          = var.aws_region
  private_subnet_ids  = module.vpc.private_subnet_ids
  public_subnet_ids   = module.vpc.public_subnet_ids
  eks_cluster_sg_id   = module.vpc.eks_cluster_sg_id
}
```

## Inputs
| Name                | Description                              | Type         | Default     |
|---------------------|------------------------------------------|--------------|-------------|
| project_prefix      | Project prefix for resource naming        | string       | n/a         |
| environment         | Deployment environment name              | string       | n/a         |
| aws_region          | AWS region for resource deployment       | string       | n/a         |
| private_subnet_ids  | List of private subnet IDs               | list(string) | n/a         |
| public_subnet_ids   | List of public subnet IDs                | list(string) | n/a         |
| eks_cluster_sg_id   | Security group ID for EKS cluster        | string       | n/a         |
| kubernetes_version  | Kubernetes version for EKS cluster       | string       | "1.29"     |
| node_instance_type  | EC2 instance type for EKS node group     | string       | "t3.medium"|
| tags                | Map of tags to apply to resources        | map(string)  | {}          |

## Outputs
| Name                | Description                              |
|---------------------|------------------------------------------|
| cluster_name        | The EKS cluster name                     |
| cluster_endpoint    | The EKS cluster endpoint                 |
| node_group_role_arn | IAM role ARN for EKS node group          |

## Requirements
- AWS CLI configured
- Terraform >= 1.4.0
- AWS provider >= 5.0

## IAM Policy
See root README for minimal IAM policy required.
