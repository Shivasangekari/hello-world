Capgemini DevOps Internship Project: CI/CD Pipeline
Prepared by: SANGEKARI SHIVANAGARAJU

Overview
In this project, I built a CI/CD pipeline for a Java web application. The main goal was to automate the entire process, from coding to deployment, using key DevOps tools.

The project started with storing the application code on GitHub for version control. A Jenkins server, hosted on an AWS computer, was set up to automatically build the application when new code was pushed. For the build process, Maven was used to package the Java code.

After the build, the application was containerized using Docker. This is a crucial step because it ensures the app runs the same way on any machine. To automate the deployment, I used Ansible to configure the servers and run the Docker container. Finally, the environment was prepared for Kubernetes (Amazon EKS) to show how the application could be managed at scale.

This automated setup resulted in a smooth, reliable, and easy-to-manage process.

Technology Used
Cloud Platform: Amazon Web Services (AWS) EC2
Version Control: Git & GitHub
CI/CD Automation Server: Jenkins
Build Tool: Apache Maven
Application Server: Apache Tomcat
Configuration Management: Ansible
Containerization: Docker
Container Registry: Docker Hub
Orchestration: Kubernetes (Amazon EKS)
SSH Client: MobaXterm
Implementation
Step 1: Initial Setup of Jenkins and Source Code
GitHub Repository: Created a repository named hello-world for storing the Java application code.
Jenkins Server on AWS: Launched an EC2 instance (t2.micro) to host Jenkins. Configured security group to allow traffic on ports 8080 and 22.
Jenkins Installation: Installed Java and Jenkins via MobaXterm. Verified Jenkins service status and completed setup in browser.
First Jenkins Job: Created a Freestyle job FirstJob to run a basic echo command. Successful output confirmed Jenkins was working.
Step 2: Automating the Application Build
Tool Installation: Installed Git and added GitHub & Maven plugins in Jenkins.
Java and Maven Configuration: Configured Java 17 and Maven paths in Jenkins Global Tool Configuration.
Build Job: Created a Maven project to pull code from GitHub and run clean install. Output: webapp.war.
Step 3: Deploying the Application with Docker and Ansible
Server Setup: Launched two EC2 instances—one for Docker Host and one for Ansible Controller.
User Configuration: Created ansadmin user with sudo access and set up passwordless SSH.
Jenkins Integration: Installed "Publish Over SSH" plugin to connect Jenkins with Docker and Ansible servers.
Deployment Job:
Transferred webapp.war to Ansible server.
Executed Ansible playbooks:
Build Docker image and push to Docker Hub.
Pull image and run container on Docker Host (port 8082 → 8080).
Verification: Confirmed container was running and application was accessible via public IP on port 8082.
Step 4: Preparing the Environment for Kubernetes
Bootstrap Server: Launched EC2 instance for EKS management.
Tool Installation: Installed aws-cli, kubectl, and eksctl.
Cluster Creation: Created IAM role with admin access and used eksctl to create EKS cluster.
Verification: Ran kubectl get nodes to confirm two nodes were created and in Ready state.
Load Balancer Access: Application accessed via external link created by Kubernetes service manifest.
Conclusion
Project Outcomes
This project was a valuable, hands-on experience. I learned how to move from just knowing about DevOps tools to using them in a practical way. A complete CI/CD pipeline was built from scratch, which showed how the entire software delivery process can be automated.

A key outcome was seeing how tools like Jenkins, Docker, and Ansible integrate to create an efficient workflow. Using Docker was especially important, as it helps ensure an application will run reliably anywhere. This project has given me a strong foundation for learning more advanced topics in the future.

Skills Gained
Setting up and configuring servers on AWS EC2
Building automated CI/CD pipelines in Jenkins
Using Maven to build and package Java applications
Creating containerized applications with Docker
Writing Ansible playbooks for server automation
Integrating different DevOps tools into a single workflow
Troubleshooting and problem-solving to fix technical issues
Challenges Faced
One of the main challenges I faced was with user permissions. For instance, the Ansible playbook failed initially because the user did not have permission to access the Docker service. I had to carefully examine the error logs to understand and fix the problem by giving the correct permissions.

This experience taught me how important it is to be patient and methodical when troubleshooting. Overcoming these challenges has made me more confident in my technical abilities.
