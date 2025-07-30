Capgemini DevOps Internship Project Report: CI/CD Pipeline
Prepared by: SANGEKARI SHIVANAGARAJU
Overview
In this project, I built a CI/CD pipeline for a Java web application. The main goal was 
to automate the entire process, from coding to deployment, using key DevOps 
tools.
The project started with storing the application code on GitHub for version control. 
A Jenkins server, hosted on an AWS computer, was set up to automatically build 
the application when new code was pushed. For the build process, Maven was used 
to package the Java code.
After the build, the application was containerized using Docker. This is a crucial 
step because it ensures the app runs the same way on any machine. To automate 
the deployment, I used Ansible to configure the servers and run the Docker 
container. Finally, the environment was prepared for Kubernetes (Amazon EKS) to 
show how the application could be managed at scale. This automated setup 
resulted in a smooth, reliable, and easy-to-manage process.
Technology Used
• Cloud Platform: Amazon Web Services (AWS) EC2
• Version Control: Git & GitHub
• CI/CD Automation Server: Jenkins
• Build Tool: Apache Maven
• Application Server: Apache Tomcat
• Configuration Management: Ansible
• Containerization: Docker
• Container Registry: Docker Hub
• Orchestration: Kubernetes (Amazon EKS)
• SSH Client: MobaXterm
Implementation
The project was implemented by following these steps.
Step 1: Initial Setup of Jenkins and Source Code
The first stage involved getting the basic tools and environment ready.
1. GitHub Repository: I used my GitHub account to create a repository 
named hello-world for storing the Java application code.
 
2. Jenkins Server on AWS: An AWS EC2 instance (t2.micro) was launched to host 
the Jenkins server. The security group was configured to allow inbound traffic 
on port 8080 for the Jenkins web UI and port 22 for SSH access.
 
3. Jenkins Installation: After connecting to the server with MobaXterm, Java and 
Jenkins were installed. I started the Jenkins service and checked its status to 
confirm it was running. The final setup steps were then completed in a web 
browser.
4. First Jenkins Job: To test that the Jenkins installation was successful, I created 
a simple Freestyle job called FirstJob. This job just ran a basic echo command. 
The successful output confirmed Jenkins was working correctly.
 
Step 2: Automating the Application Build
The next step was to configure Jenkins to build the application from the source 
code automatically.
1. Tool Installation: Git was installed on the Jenkins server. From the Jenkins 
dashboard, the GitHub and Maven Integration plugins were added to extend 
its functionality.
2. Java and Maven Configuration: In the Jenkins 'Global Tool Configuration' 
settings, I added the paths for the Java 17 and Maven installations. This allows 
Jenkins to find and use these tools during the build process.

3. Building the Project with Maven: A new 'Maven project' was created in 
Jenkins. It was configured to pull code from the GitHub repository and execute 
the clean install Maven command. The job ran successfully, producing 
a webapp.war file as the build artifact.
Step 3: Deploying the Application with Docker and Ansible
This stage focused on containerizing the built application and automating its 
deployment.
1. Docker and Ansible Server Setup: Two new EC2 instances were launched: one 
to serve as a Docker Host and the other as an Ansible Controller. Docker was 
installed on the Docker Host, while Ansible was installed on the Ansible 
Controller.

2. Connecting Ansible to Docker Host: On the Docker Host, I created a user 
named ansadmin and granted it sudo privileges. Then, a passwordless SSH 
connection was set up from the Ansible Controller to the Docker Host. A 
successful test was performed using the ansible all -m ping command.
3. Linking Jenkins to Docker and Ansible: The "Publish Over SSH" plugin was 
installed in Jenkins. It was configured with the Docker’s and Ansible server's IP 
address and username to allow Jenkins to send files to it.
4. Creating the Main Deployment Job: A new Jenkins job was created to handle 
the full CI/CD workflow.
o As a post-build action, the job was configured to transfer 
the webapp.war file to the Ansible server.
o Following the file transfer, a shell command was added to execute the 
Ansible playbooks.

5. Running the Ansible Playbooks:
o The first playbook built a Docker image of the application and pushed it 
to my account on Docker Hub.
o The second playbook pulled the latest image from Docker Hub and ran it 
as a new container on the Docker Host, mapping port 8082 on the host 
to port 8080 in the container.
Final Deployment Verification: The Jenkins job completed successfully. I checked 
the Docker Host and confirmed the new container was running. The application 
was then accessible in a web browser using the server's public IP on port 8082.
Step 4: Preparing the Environment for Kubernetes
The final step was to set up the tools needed to manage the application using 
Kubernetes.
1. EKS Bootstrap Server: A new EC2 instance was launched to act as a 
bootstrap server for managing the Amazon EKS cluster.
2. Kubernetes Tool Installation: The necessary command-line tools (awscli, kubectl, and eksctl) were installed on the bootstrap server.
3. EKS Cluster Creation: An IAM role with administrator access was created 
and attached to the bootstrap server. This granted eksctl the permissions 
needed to create AWS resources. eksctl was then used to create the EKS 
cluster successfully.
In below you can see cluster has been created and you can also see after executing 
kubectl get nodes it showing two nodes created and status is ready
Above pic is been accessed using External link of load balancer, these load balancer 
is created when I created service manifest file in eks
Conclusion
Project Outcomes
This project was a valuable, hands-on experience. I learned how to move from just 
knowing about DevOps tools to using them in a practical way. A complete CI/CD 
pipeline was built from scratch, which showed how the entire software delivery 
process can be automated. A key outcome was seeing how tools like Jenkins, 
Docker, and Ansible integrate to create an efficient workflow. Using Docker was 
especially important, as it helps ensure an application will run reliably anywhere. 
This project has given me a strong foundation for learning more advanced topics in 
the future.
Skills Gained
• Setting up and configuring servers on AWS EC2.
• Building automated CI/CD pipelines in Jenkins.
• Using Maven to build and package Java applications.
• Creating containerized applications with Docker.
• Writing Ansible playbooks for server automation.
• Integrating different DevOps tools into a single workflow.
• Troubleshooting and problem-solving to fix technical issues.
Challenges Faced
One of the main challenges I faced was with user permissions. For instance, the 
Ansible playbook failed initially because the user did not have permission to access 
the Docker service. I had to carefully examine the error logs to understand and fix 
the problem by giving the correct permissions. This experience taught me how 
important it is to be patient and methodical when troubleshooting. Overcoming 
these challenges has made me more confident in my technical abilities.
