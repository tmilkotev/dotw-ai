# dotw-terraform — Master Prompt

## Context

dotw-terraform is part of the DevOpsTheWay (DOTW) ecosystem.

It provides Terraform-based AWS infrastructure for a multi-account lab environment designed for learning, experimentation, and preparation for real-world SRE roles.

The focus is on:

- practical AWS usage
- clean Terraform design
- cost awareness
- production-inspired architecture without unnecessary complexity

---

## Architecture Overview

The system uses a multi-account AWS setup.

Accounts and responsibilities:

management → AWS Organizations, IAM Identity Center, budgets, alerts  
network → VPC, subnets, routing, internet gateway, NACLs  
workload → EC2, IAM roles, security groups, CloudWatch  
security → minimal initially, later CloudTrail and security services  

Key principles:

- clear separation of concerns per account
- Terraform executed per account (no platformctl integration yet)
- reusable modules + simple root compositions
- foundation-first approach

---

## v0.1.0 Scope

management:
- AWS Organizations
- IAM Identity Center
- AWS Budgets
- budget alerts

network:
- VPC
- public subnets
- internet gateway
- route tables
- NACLs (basic)

workload:
- EC2 (t3.micro or equivalent)
- IAM roles / instance profiles
- Security Groups
- CloudWatch basics (metrics + simple alarms)

security:
- account exists
- CloudTrail optional and minimal

Constraints:

- no NAT Gateway
- no load balancers
- no EKS
- no always-on paid services
- keep everything within free-tier or near-zero cost

---

## Later Expansion

management:
- permission sets refinement
- governance patterns

network:
- private subnets
- VPC peering (if needed)
- Route 53 (if needed)

workload:
- Lambda
- S3
- DynamoDB
- RDS (controlled usage)
- automation (start/stop)
- richer monitoring

security:
- CloudTrail full setup
- guardrails
- AWS Config (only when intentionally needed)

---

## Terraform Design Principles

- modules are small, reusable building blocks
- accounts are root modules composing those blocks
- avoid over-abstraction
- prefer clarity over flexibility
- no hidden logic
- no unnecessary variables
- everything should be understandable by reading Terraform directly

---

## IAM Model

- AWS Organizations + IAM Identity Center for human access
- IAM roles for workloads (EC2, Lambda)
- no centralized IAM complexity beyond Identity Center in v0.1.0
- no hardcoded credentials

---

## Cost Model

- strict cost awareness
- prefer free-tier services
- EC2 must be stoppable
- avoid services with baseline hourly cost
- budgets and alerts are mandatory from the start

---

## Mental Model

management → who can access and what it costs  
network → where things live  
workload → what runs  
security → who did what (later)

---

## Expectations for Responses

- do not overengineer
- do not introduce unnecessary services
- keep solutions aligned with v0.1.0 unless explicitly asked
- prefer incremental, buildable steps
- highlight cost implications when relevant
- challenge decisions if they introduce unnecessary complexity