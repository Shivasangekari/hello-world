# Capgemini DevOps Internship Project: CI/CD Pipeline

**Prepared by:** SANGEKARI SHIVANAGARAJU  
**Role:** Software Engineer  
**Location:** Hyderabad, Telangana  

## Overview

This project demonstrates the implementation of a complete CI/CD pipeline for a Java web application. The goal was to automate the software development lifecycle—from code commit to deployment—using industry-standard DevOps tools.

The pipeline includes:
- Version control with GitHub
- Continuous integration with Jenkins
- Build automation using Maven
- Containerization with Docker
- Configuration management via Ansible
- Orchestration using Kubernetes (Amazon EKS)

---

##  Technologies Used

| Category                  | Tools/Platforms                     |
|---------------------------|-------------------------------------|
| Cloud Platform            | AWS EC2                             |
| Version Control           | Git, GitHub                         |
| CI/CD Automation          | Jenkins                             |
| Build Tool                | Apache Maven                        |
| Application Server        | Apache Tomcat                       |
| Configuration Management  | Ansible                             |
| Containerization          | Docker                              |
| Container Registry        | Docker Hub                          |
| Orchestration             | Kubernetes (Amazon EKS)             |
| SSH Client                | MobaXterm                           |

---

## Implementation Steps

### Step 1: Jenkins & Source Code Setup

- **GitHub Repository**: Created `hello-world` repo for Java application.
- **Jenkins Server**: Launched EC2 instance (t2.micro) with ports 8080 (Jenkins UI) and 22 (SSH).
- **Installation**: Installed Java and Jenkins via MobaXterm.
- **First Jenkins Job**: Created a Freestyle job `FirstJob` to verify Jenkins setup.

### Step 2: Automating the Build Process

- **Tool Setup**: Installed Git, Maven, and required Jenkins plugins.
- **Global Tool Configuration**: Added Java 17 and Maven paths.
- **Build Job**: Created a Maven project in Jenkins to pull code from GitHub and run `clean install`. Output: `webapp.war`.

### Step 3: Deployment with Docker & Ansible

- **Server Setup**: Launched two EC2 instances for Docker Host and Ansible Controller.
- **User Configuration**: Created `ansadmin` user with sudo access and set up passwordless SSH.
- **Jenkins Integration**: Installed "Publish Over SSH" plugin to connect Jenkins with Docker and Ansible servers.
- **Deployment Job**:
  - Transferred `webapp.war` to Ansible server.
  - Executed Ansible playbooks:
    - Build Docker image and push to Docker Hub.
    - Pull image and run container on Docker Host (port 8082 → 8080).

### Step 4: Kubernetes (Amazon EKS) Setup

- **Bootstrap Server**: Launched EC2 instance for EKS management.
- **Tool Installation**: Installed `aws-cli`, `kubectl`, and `eksctl`.
- **Cluster Creation**:
  - Created IAM role with admin access.
  - Used `eksctl` to create EKS cluster.
  - Verified with `kubectl get nodes` (2 nodes in Ready state).
- **Load Balancer Access**: Application accessed via external link created by Kubernetes service manifest.

---

##  Project Outcomes

- Built a fully automated CI/CD pipeline from scratch.
- Gained hands-on experience with Jenkins, Docker, Ansible, and Kubernetes.
- Demonstrated how DevOps tools integrate to streamline software delivery.
- Ensured consistent deployment using Docker containers.

---

##  Skills Gained

- AWS EC2 provisioning and configuration
- Jenkins pipeline creation and management
- Maven-based Java application builds
- Docker image creation and container management
- Writing and executing Ansible playbooks
- Kubernetes cluster setup and deployment
- Troubleshooting and debugging DevOps workflows

---

##  Challenges Faced

- **Permission Issues**: Ansible playbook initially failed due to insufficient Docker access. Resolved by adjusting user permissions.
- **Troubleshooting**: Learned to analyze logs and apply methodical debugging techniques.

---

##  Conclusion

This internship project provided a solid foundation in DevOps practices and tools. It bridged the gap between theoretical knowledge and real-world implementation, preparing me for more advanced DevOps challenges in the future.

---

