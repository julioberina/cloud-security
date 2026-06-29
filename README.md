# ☁️ Cloud Security Engineering Journey

This repository serves as a technical log of my transition from **Senior Software Engineer** to **Cloud Security Engineer**. It documents my pursuit of deep AWS architectural knowledge, hands-on vulnerability research, and the application of security best practices in cloud-native environments.

## 🎯 Background
6+ years of full-stack and backend engineering experience across Java/Spring Boot, Angular, and DevSecOps pipelines. Currently leveraging that foundation to specialize in cloud security architecture, IAM, and infrastructure hardening on AWS.

## 🏗️ Repository Structure
- `/aws-saa` — Technical breakdowns of AWS services, architectural patterns, and demo notes aligned with the Cantrill SAA-C03 course.
- `/flaws2-cloud` — Structured security lab write-ups from [flaws2.cloud](http://flaws2.cloud), focusing on attack paths, root cause analysis, and defensive remediation.
- `/projects` — (Coming Soon) Terraform-based security baselines and automated incident response scripts.

## 🛡️ Featured Write-ups
- **[Flaws2.cloud Level 1: Credential Leaks via API Gateway](./flaws2-cloud/level1.md)** — How improper error handling exposes temporary STS credentials and how to prevent it.

## 📜 Certification Path
- ✅ CompTIA Security+ (Feb 2026)
- ⏳ AWS Solutions Architect Associate — SAA-C03 (Est. Q3 2026)
- 🔜 AWS Certified Security – Specialty

## ⚠️ Disclaimer
All security research in this repository was performed in intentionally vulnerable, sandboxed lab environments (flaws2.cloud). No real systems were targeted. Sensitive-looking values such as access keys have been redacted or replaced with placeholders.

---

### 🟦 Phase 1: AWS Foundation & IAM Specialization (8-10 Weeks)
**Goal:** Master the AWS control plane. Understand not just *how* to build, but *how* identities interact and where they fail.

#### 🔲 PRE-START: Setup & Head Start (This Week)
*   [x] Set up AWS Study Notebook (Apple Notes/Obsidian).
*   [x] Create/Secure AWS Lab Account (Enable MFA immediately).
*   [x] Configure AWS CLI v2 and verify with `aws configure`.
*   [x] **Cantrill:** Watch/Note: *AWS Accounts Basics, MFA, IAM Basics, IAM Access Keys*.
*   [x] **flaws2.cloud:** Begin the **Attacker** path. 
    *   *Note format: What identity did I get? What permission allowed the pivot?*

---

#### 🔲 WEEK 1: The Basics & Shared Responsibility
*   **Focus:** Core infrastructure and the "Security OF the Cloud" vs "Security IN the Cloud."
*   [x] **Cantrill:** *AWS Fundamentals (Global Infra, Public vs Private, Default VPC, EC2/S3 Basics).*
*   [ ] **Cantrill:** *Shared Responsibility Model, High-Availability vs Disaster Recovery.*
*   [ ] **Note:** Compare Region vs. AZ from a security/compliance perspective.
*   [ ] **flaws2.cloud:** 1 session.

#### 🔲 WEEK 2: The Heart of the Pivot (IAM & ORGS)
*   **Focus:** This is your most important week. Treat Policies like code.
*   [ ] **Cantrill:** *IAM Identity Policies, Users/ARNs, Groups, Roles (Tech & Use Cases).*
*   [ ] **Cantrill:** *Service-linked Roles & PassRole (Critical security topic).*
*   [ ] **Cantrill:** *AWS Organizations & Service Control Policies (SCPs).*
*   [ ] **Cantrill:** *CloudWatch Logs & CloudTrail (Detection & Audit).*
*   [ ] **Deep Dive:** Research "IAM Policy Evaluation Logic" (Explicit Deny vs. Allow).
*   [ ] **flaws2.cloud:** 1 session.

#### 🔲 WEEK 3: S3 & Data Security (KMS)
*   **Focus:** S3 is the #1 source of cloud leaks. Master its specific access controls.
*   [ ] **Cantrill:** *S3 Security (Resource Policies vs. ACLs), Versioning, MFA Delete.*
*   [ ] **Cantrill:** *Key Management Service (KMS) & Object Encryption (SSE-KMS/SSE-S3).*
*   [ ] **Cantrill:** *PreSigned URLs & S3 Access Points.*
*   [ ] **Deep Dive:** S3 Block Public Access vs. Bucket Policies.
*   [ ] **flaws2.cloud:** 1 session.

#### 🔲 WEEK 4: Networking & Trust Boundaries (VPC)
*   **Focus:** Segmentation and network-level isolation.
*   [ ] **Cantrill:** *VPC Sizing, Subnets (Public vs Private), Routing, Internet Gateways.*
*   [ ] **Cantrill:** *Security Groups vs. NACLs (Stateful vs. Stateless).*
*   [ ] **Cantrill:** *NAT Gateways & Bastion Hosts.*
*   [ ] **Deep Dive:** Draw a 3-tier VPC diagram labeling every security boundary.
*   [ ] **flaws2.cloud:** 1 session.

#### 🔲 WEEK 5: Compute Security & Instance Roles
*   **Focus:** The "Compute" layer. How attackers jump from code to the Cloud API.
*   [ ] **Cantrill:** *Instance Metadata Service (IMDSv1 vs v2 security implications).*
*   [ ] **Cantrill:** *EC2 Instance Roles & Profiles (Metadata attack surface).*
*   [ ] **Cantrill:** *SSM Parameter Store (Safe secret injection).*
*   [ ] **Cantrill:** *CloudWatch Agent (Logging system-level logs to the cloud).*
*   [ ] **Deep Dive:** Compare "Secrets in UserData" vs. "Secrets in Parameter Store."

#### 🔲 WEEK 6: Architecture & Operational Security
*   **Focus:** High-traffic patterns and internet-facing security.
*   [ ] **Cantrill:** *Route 53 (DNSSEC, Health Checks).*
*   [ ] **Cantrill:** *RDS Security (Network placement, Encryption at Rest/Transition).*
*   [ ] **Cantrill:** *ELB (ALB/NLB) & SSL/TLS termination.*
*   [ ] **Cantrill:** *CloudFront & WAF / Shield (Edge security).*
*   [ ] **Note:** How does an ALB with a WAF protect the VPC?

#### 🔲 WEEK 7: Serverless & Security Services
*   **Focus:** Modern app security and the "Security Service" suite.
*   [ ] **Cantrill:** *Lambda Security (Execution roles, VPC vs. non-VPC).*
*   [ ] **Cantrill:** *API Gateway & Cognito (Authentication/Identity Pools).*
*   [ ] **Cantrill:** *GuardDuty, Inspector, Macie, Config (Building the "Defense" toolbelt).*
*   [ ] **Deep Dive:** Contrast GuardDuty (Detective) with WAF (Preventative).

#### 🔲 WEEK 8: Automation & Capstone Project
*   **Focus:** Infrastructure as Code (IaC) and combining everything.
*   [ ] **Cantrill:** *CloudFormation (Physical vs Logical, Stack Roles, Custom Resources).*
*   [ ] **Cantrill:** *VPC Endpoints & Peering (Private connectivity).*
*   [ ] **Project:** BUILD THE CROSS-ACCOUNT ACCESS DEMO (Notes/GitHub).
*   [ ] **Review:** Take 1 Practice Exam to find knowledge gaps.
*   [ ] **Decision:** Book SAA-C03 Cert (Yes/No).

---

### 📝 The "Security Engineer" Note Template
*Copy this for your Apple Notes and paste it for each main service/lesson:*

*   **Service Name:**
*   **What is it?** (1 sentence):
*   **Identity:** What principal/role touches this?
*   **Access Control:** Is it Identity-policy, Resource-policy, or Networking-based?
*   **Misconfiguration:** What is the "Classic Steve" mistake here? (e.g. S3 Public, "*" Action)
*   **Blast Radius:** If an attacker gets these keys, what else can they kill/steal?
*   **Detection:** Which log (CloudTrail, VPC Flow, etc) proves the activity?
*   **Hardening:** One-sentence fix for the misconfiguration.