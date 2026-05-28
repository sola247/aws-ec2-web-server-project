# AWS EC2 Web Server Infrastructure Project

A hands-on portfolio project demonstrating fundamental cloud infrastructure concepts using Amazon Web Services (AWS). This project focuses on deploying and managing a production-ready web server on EC2 instances with proper networking, security, and scalability considerations.

---

## 📋 Project Overview

This project showcases practical skills in cloud infrastructure development by building a secure, scalable web server environment on AWS. It serves as a learning resource and portfolio demonstration for deploying real-world cloud applications using industry best practices.

**Project Type:** Cloud Infrastructure / Infrastructure as Code (IaC) - Beginner  
**Target Audience:** Cloud engineering beginners, DevOps enthusiasts, and portfolio builders

---

## ☁️ AWS Services Used

- **Amazon EC2** - Compute instances for web server hosting
- **Amazon VPC** - Virtual private cloud networking
- **Security Groups** - Firewall rules and network access control
- **Elastic IPs** - Static IP addressing (optional)
- **Amazon Linux / Ubuntu** - Linux-based operating systems
- **IAM Roles & Policies** - Instance permissions and access management

---

## 🎯 Project Goals

- [ ] Deploy a Linux-based EC2 instance in a custom VPC
- [ ] Configure Security Groups with appropriate inbound/outbound rules
- [ ] Install and configure a web server (Apache/Nginx)
- [ ] Implement basic networking principles (subnets, routing)
- [ ] Demonstrate SSH key-based authentication
- [ ] Document infrastructure setup and deployment procedures
- [ ] Implement security best practices for production readiness
- [ ] Create reusable scripts for infrastructure deployment

---

## 🏗️ Planned Architecture

### High-Level Architecture Diagram

```
[Internet Gateway]
        |
    [Route Table]
        |
  [Public Subnet]
        |
  [EC2 Instance]
   (Web Server)
        |
 [Security Group]
  (Firewall Rules)
```

**Architecture Components:**

1. **VPC (Virtual Private Cloud)** - Isolated network environment
2. **Public Subnet** - EC2 instance accessible from the internet
3. **Internet Gateway** - Gateway for internet connectivity
4. **Security Group** - Stateful firewall controlling traffic
5. **EC2 Instance** - Compute resource running web server software
6. **Key Pair** - SSH authentication credentials

### Network Flow

```
User Request (HTTP/HTTPS)
        ↓
Internet Gateway
        ↓
Route Table (0.0.0.0/0 → IGW)
        ↓
Security Group (Inbound: 80, 443, 22)
        ↓
EC2 Instance
        ↓
Web Server (Apache/Nginx)
        ↓
Application Response
```

---

## 🚀 Deployment Steps

### Prerequisites
- AWS Account with appropriate IAM permissions
- AWS CLI configured locally
- SSH client installed
- Basic Linux command-line knowledge

### Step 1: VPC and Networking Setup
```bash
# Create custom VPC
# Create public subnet
# Create Internet Gateway
# Configure route table
```

### Step 2: Security Group Configuration
```bash
# Create Security Group
# Inbound Rules:
#   - SSH (Port 22) - Source: Your IP or 0.0.0.0/0 for testing
#   - HTTP (Port 80) - Source: 0.0.0.0/0
#   - HTTPS (Port 443) - Source: 0.0.0.0/0
# Outbound Rules: All traffic allowed
```

### Step 3: EC2 Instance Launch
```bash
# Launch EC2 instance
# - AMI: Amazon Linux 2 or Ubuntu 20.04 LTS
# - Instance Type: t2.micro (eligible for free tier)
# - VPC: Custom VPC created above
# - Subnet: Public subnet
# - Auto-assign Public IP: Enable
# - Attach Security Group
# - Generate or import Key Pair
```

### Step 4: Connect to Instance
```bash
# SSH into instance
ssh -i /path/to/key-pair.pem ec2-user@<instance-public-ip>

# Or for Ubuntu
ssh -i /path/to/key-pair.pem ubuntu@<instance-public-ip>
```

### Step 5: Web Server Installation
```bash
# Update system packages
sudo yum update -y  # Amazon Linux
# OR
sudo apt update && sudo apt upgrade -y  # Ubuntu

# Install web server
sudo yum install -y httpd  # Amazon Linux
# OR
sudo apt install -y apache2  # Ubuntu

# Start and enable service
sudo systemctl start httpd
sudo systemctl enable httpd

# Verify installation
curl http://localhost
```

### Step 6: Deploy Application
```bash
# Create sample web content
sudo bash -c 'echo "<h1>Web Server Running on EC2</h1>" > /var/www/html/index.html'

# Access via browser
# http://<instance-public-ip>
```

---

## 🔐 Security Considerations

### Network Security
- ✅ **Security Groups** - Implement least privilege principle
  - Only expose necessary ports (80, 443, 22)
  - Restrict SSH access to known IPs when possible
  - Deny all inbound by default, explicitly allow required traffic

- ✅ **Network ACLs** - Stateless firewall for subnet-level control
  - Implement additional layer of network security
  - Configure deny rules for known malicious traffic

### Instance Security
- ✅ **SSH Key Management**
  - Use strong, unique key pairs
  - Store private keys securely (never commit to version control)
  - Rotate keys periodically
  - Disable password-based SSH authentication

- ✅ **Operating System Hardening**
  - Keep systems patched and updated regularly
  - Disable unnecessary services
  - Configure host-based firewall (iptables/firewalld)
  - Implement fail2ban for SSH protection

### Access Control
- ✅ **IAM Roles and Policies**
  - Use IAM roles instead of hardcoded credentials
  - Follow principle of least privilege
  - Enable CloudTrail for audit logging

- ✅ **Monitoring and Logging**
  - Enable VPC Flow Logs for network traffic analysis
  - Configure CloudWatch alarms for security events
  - Enable EC2 detailed monitoring

### Application Security
- ✅ **Web Server Configuration**
  - Run web server as non-root user
  - Implement HTTPS with SSL/TLS certificates
  - Configure security headers
  - Regular security patching

### Best Practices
- Never use default credentials
- Implement multi-factor authentication (MFA) for AWS accounts
- Use AWS Secrets Manager for sensitive data
- Regularly audit security group rules
- Document all security configurations

---

## 📊 Current Status

### Project Phase: Initial Setup

- [x] Repository initialized
- [ ] VPC and networking infrastructure
- [ ] Security groups configuration
- [ ] EC2 instance deployment
- [ ] Web server installation
- [ ] Application deployment
- [ ] Monitoring and logging setup
- [ ] Documentation completion

### Progress: 10%

---

## 📁 Repository Structure

```
aws-ec2-web-server-project/
├── README.md                          # Project documentation
├── docs/
│   ├── ARCHITECTURE.md                # Detailed architecture documentation
│   ├── DEPLOYMENT_GUIDE.md            # Step-by-step deployment instructions
│   └── TROUBLESHOOTING.md             # Common issues and solutions
├── scripts/
│   ├── vpc-setup.sh                   # VPC creation script
│   ├── security-group-setup.sh        # Security group configuration
│   ├── ec2-launch.sh                  # EC2 instance launch script
│   └── web-server-setup.sh            # Web server installation script
├── infrastructure/
│   ├── terraform/                     # Infrastructure as Code (IaC)
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── cloudformation/                # CloudFormation templates
│       └── web-server-stack.yaml
├── config/
│   ├── apache-config.conf             # Web server configuration
│   ├── security-hardening.sh          # Security hardening script
│   └── monitoring-setup.sh            # CloudWatch monitoring script
├── screenshots/                        # Architecture and deployment screenshots
│   ├── architecture-diagram.png
│   └── deployment-steps.png
└── .gitignore                         # Git ignore rules
```

---

## 📚 Learning Resources

- [AWS EC2 Documentation](https://docs.aws.amazon.com/ec2/)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [AWS Security Best Practices](https://aws.amazon.com/architecture/security-identity-compliance/)
- [Linux System Administration Basics](https://linux.com/training/)
- [SSH Key Management](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html)

---

## 🔧 Technologies & Tools

- **Cloud Platform:** Amazon Web Services (AWS)
- **Compute:** EC2 (t2.micro)
- **Operating System:** Amazon Linux 2 / Ubuntu 20.04 LTS
- **Web Server:** Apache HTTP Server / Nginx
- **Infrastructure as Code:** Terraform / CloudFormation (future)
- **Monitoring:** AWS CloudWatch
- **Version Control:** Git / GitHub

---

## 💡 Key Concepts Demonstrated

| Concept | Details |
|---------|---------|
| **Cloud Computing** | On-demand compute resources in a managed environment |
| **Virtualization** | Running multiple instances on shared hardware |
| **Networking** | VPC design, subnets, routing, and internet connectivity |
| **Security** | Firewalls, access control, encryption, and authentication |
| **Infrastructure as Code** | Automating infrastructure provisioning |
| **Scalability** | Designing systems to handle growth |
| **High Availability** | Building resilient and fault-tolerant systems |

---

## 🎓 Skill Development

This project helps develop proficiency in:

- ✅ AWS core services (EC2, VPC, Security Groups)
- ✅ Cloud networking fundamentals
- ✅ Linux/Unix system administration
- ✅ Web server configuration and management
- ✅ Security best practices in cloud environments
- ✅ Cloud infrastructure documentation
- ✅ Troubleshooting cloud deployments

---

## 📝 Future Enhancements

- [ ] Implement Auto Scaling Groups for high availability
- [ ] Add Application Load Balancer for traffic distribution
- [ ] Deploy using Infrastructure as Code (Terraform/CloudFormation)
- [ ] Implement CI/CD pipeline for application deployment
- [ ] Add RDS database integration
- [ ] Implement S3 for static file storage
- [ ] Configure CloudFront CDN
- [ ] Add SNS notifications for system alerts
- [ ] Implement Systems Manager for instance management
- [ ] Create disaster recovery procedures

---

## 🤝 Contributing

This is a personal portfolio project. For suggestions or improvements, feel free to fork and create your own version.

---

## 📄 License

This project is open source and available under the MIT License. See LICENSE file for details.

---

## ✉️ Contact & Social

- **GitHub:** [@sola247](https://github.com/sola247)
- **Portfolio:** [Your Portfolio Link]
- **LinkedIn:** [Your LinkedIn Profile]

---

## 📖 Additional Notes

### For Recruiters

This project demonstrates:
- Hands-on experience with AWS cloud platform
- Understanding of cloud networking and security
- Linux system administration capabilities
- Infrastructure automation knowledge
- Clear technical documentation skills
- Portfolio-ready project structure

### Version History

- **v1.0** (2026-05-28) - Initial project setup and documentation

---

**Last Updated:** 2026-05-28  
**Project Status:** Active Development
