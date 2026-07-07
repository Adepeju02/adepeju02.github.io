---
title: "AWS ALB & RDS Troubleshooting"
category: "Cloud Security"
tools: "AWS (EC2, ALB, RDS/MariaDB, VPC, IAM) · PHP · mysqli · Linux"
excerpt: "Diagnosed and corrected an internal-facing ALB misconfiguration and resolved TLS-enforced RDS connectivity by reconfiguring both infrastructure routing and application-layer SSL handling."
header:
  teaser: /assets/images/projects/aws-alb-placeholder.png
---

**Category:** Cloud Security / Infrastructure  
**Tools:** AWS (EC2, ALB, RDS/MariaDB, VPC, IAM) · PHP · mysqli · Linux

---

## Objective

Diagnose and fix a misconfigured Application Load Balancer and resolve SSL/TLS-enforced database connectivity failures in a live multi-tier web application.

## What I Did

- Identified that the ALB was configured as internal-facing instead of internet-facing; rebuilt it with correct public subnet associations to restore public traffic routing
- Diagnosed why a PHP application was failing to connect to RDS: MariaDB had `require_secure_transport=ON`, blocking all non-SSL MySQL connections
- Used `--ssl-ca=` flags to complete a data import over SSL
- Modified three PHP files (`menu.php`, `processOrder.php`, `orderHistory.php`) to explicitly call `mysqli_ssl_set()` with `MYSQLI_CLIENT_SSL`, enabling the application to connect securely without disabling server-side enforcement
- Identified that IAM permissions blocked disabling SSL enforcement at the parameter group level — implemented and documented an application-layer workaround rather than suppressing the constraint

## Challenges & How I Solved Them

- **IAM permission boundary:** Could not disable `require_secure_transport` at the RDS parameter group level due to IAM restrictions. Rather than flagging the task as incomplete, implemented the fix at the application layer and documented exactly why the infrastructure-level path was blocked — demonstrating constraint-aware troubleshooting.

## Outcome

ALB correctly routing public traffic; PHP application connecting to RDS over enforced TLS with proper SSL context configured at the application layer — no security enforcement bypassed.

## Skills Demonstrated

AWS networking (VPC, subnets, ALB) · RDS/MySQL TLS configuration · IAM permissions analysis · Application-layer SSL remediation · Cloud troubleshooting methodology · PHP/mysqli SSL setup

{% include figure image_path="/assets/images/projects/aws-alb-placeholder.png" alt="AWS ALB configuration and RDS connectivity" caption="AWS console showing ALB and RDS configuration — replace with your screenshot" %}
