 Azure Linux VM Deployment with SSH Key Authentication

 📌 Project Overview
This project demonstrates secure deployment of an Ubuntu Linux VM in Azure using industry-standard SSH key authentication. The focus was on implementing security best practices, understanding cloud authentication methods, and documenting the complete infrastructure lifecycle.

**All resources were properly deleted at Resource Group level to ensure cost optimization and cloud hygiene.**



 Objectives
- Deploy Ubuntu Linux VM 24.04 LTS using Azure Portal
- Implement SSH key pair authentication (security best practice)
- Configure Network Security Groups with single-port access
- Establish secure remote connection using correct OS-specific credentials
- Document the discovery process for Azure's authentication patterns
- Execute proper cloud resource teardown at Resource Group level



 Architecture & Services
Azure Services Utilized:
- Azure Virtual Machine (Ubuntu Server 24.04 LTS)
- Resource Groups (Logical container for lifecycle management)
- Virtual Network & Subnet
- Network Security Group (NSG) with SSH-only rule
- Public IP Address
- SSH Key Pair Authentication

Security Configuration:
- Authentication: SSH Public Key (Eliminates password vulnerabilities)
- Inbound Access: Port 22 (SSH) only via NSG
- Key Management: Secure .pem file with user-only permissions
- Default Credentials: Validated OS-specific username patterns



 Technical Configuration

Region: South Africa North 
VM Size: Standard_B2ats_v2 (2 vCPU, 1 GiB RAM) 
OS Image: Ubuntu Server 24.04 LTS 
Authentication: SSH Public Key (Generated in Azure)
Disk Type: Standard SSD 
Public IP: Dynamic (102.133.161.26) 
Username: azureuser (validated working credential) 
Availability: No infrastructure redundancy required 



Secure Access Implementation

 SSH Key Authentication Workflow:
1. Key Generation: Created new SSH key pair within Azure Portal
2. Private Key Security: Downloaded .pem file to secure local storage (Mfaniseni-VM.pem)
3. Public Key Deployment: Azure automatically injected public key to VM
4. Credential Validation: Tested authentication with OS-specific username

Successful Connection Command:
`bash
Navigate to key directory
cd Downloads

 Establish secure SSH connection
ssh -i Mfaniseni-VM.pem azureuser@102.133.161.26

# Accept host fingerprint for first connection
The authenticity of host '102.133.161.26' can't be established...
Are you sure you want to continue connecting (yes/no)? yes
 Screenshot 1: Resource Group Creation & Naming Convention
https://01-resource-group.png

 Screenshot 2: SSH Key Pair Generation Interface
https://02-ssh-key-config.png

 Screenshot 5: Successful SSH Connection Terminal
https://05-ssh-success.png

 Technical Discovery & Validation
Credential Pattern Investigation:
During implementation, I explored Azure's authentication defaults across different Ubuntu versions:

Discovery Process:

Initial Hypothesis: Azure uses consistent credentials across Linux distributions

Documentation Analysis: Compared lab instructions (Ubuntu 20.04) with actual deployment (24.04)

Empirical Testing: Validated azureuser as working credential through connection testing

Platform Understanding: Recognized cloud providers adapt defaults based on OS security recommendations

Key Insight:
Cloud platforms evolve authentication methods, requiring technicians to validate current behavior rather than relying solely on historical documentation.

 Screenshot 3: NSG Configuration with SSH Rule
https://03-nsg-configuration.png

 Screenshot 4: Key Download Confirmation Dialog
https://04-key-download.png

Security Architecture
Network Security Group Configuration:
Rule Type: Inbound security rule

Service: SSH

Protocol: TCP

Port: 22

Source: Any (Internet)

Priority: 300

Action: Allow

Security Advantages Demonstrated:
No Password Storage: Eliminates credential database vulnerabilities

Cryptographic Security: 2048-bit RSA key pair authentication

Minimal Attack Surface: Single exposed port with key-based access

Personal Key Management: Private key never leaves user control

Identified Production Considerations:
SSH port 22 exposed to internet (authenticated but visible)

No Just-In-Time (JIT) access implementation

No network-level logging or intrusion detection

 Cloud Resource Management
Proper Cleanup Methodology:
Learning Moment: Initial VM-only deletion versus complete Resource Group cleanup

Correct Implementation:

Navigated to Resource Groups (not individual VM)

Selected target Resource Group (RG-Linux-Lab-01-31)

Executed Resource Group deletion

Verified all associated resources removed:

Virtual Machine

Virtual Network

Network Security Group

Public IP Address

OS Disk

Best Practice Established: Always delete at Resource Group level for complete resource lifecycle management.

 Screenshot 6: Resource Group Deletion Confirmation
https://06-cleanup.png

 Skills Demonstrated & Career Relevance
Technical Competencies:
Cloud Security: SSH key authentication implementation and management

Azure IaaS: Linux VM deployment, configuration, and lifecycle management

Networking: NSG configuration and cloud network security principles

Troubleshooting: Systematic approach to cloud connectivity and authentication

Documentation: Professional technical documentation with visual aids

Professional Skills:
Problem-Solving: Investigative approach to technical challenges

Adaptability: Adjusting to platform updates and version differences

Best Practices: Implementing industry security standards

Cost Management: Proper resource teardown and cloud hygiene

Target Roles Enhanced:
Cloud Support Engineer

DevOps Engineer (Infrastructure focus)

Cloud Security Analyst

Linux System Administrator (Cloud environment)

Site Reliability Engineer (SRE)

⚡ Comparison with Windows VM Project
Aspect	Windows VM Project	Linux VM Project
Authentication	Password-based (Complex)	SSH Key-based (Cryptographic)
Protocol	RDP (3389)	SSH (22)
Security Level	Basic (Industry baseline)	Enhanced (Industry standard)
Access Method	GUI Remote Desktop	CLI Terminal
Skill Development	Cloud Fundamentals	Security Best Practices
Progression Demonstrated: From basic cloud VM deployment to security-focused implementation.
