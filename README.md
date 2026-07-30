# Elevance DevOps CI/CD Project

## Project Overview

This project was completed as part of the Elevance DevOps Internship. The objective was to automate the deployment of a static HTML/CSS website on AWS using DevOps tools and practices.

The project covers Infrastructure as Code (Terraform), Configuration Management (Ansible), Containerization (Docker), Continuous Integration (Jenkins), and deployment on an AWS EC2 instance.

---

## Technologies Used

* AWS EC2
* Terraform
* Ansible
* Docker
* Docker Compose
* Jenkins
* GitHub
* Docker Hub
* HTML
* CSS

---

## Project Structure

```text
Elevance-CI-CD
│
├── Terraform/
├── Ansible/
├── Docker/
├── Website/
├── Jenkinsfile
└── README.md
```

---

## Task 1 – Infrastructure Provisioning using Terraform

Terraform was used to create the AWS infrastructure required for deployment.

### Resources Created

* EC2 Instance (t3.micro)
* Security Group
* SSH (Port 22)
* HTTP (Port 80)
* TCP (Port 8080)

### Commands Used

```bash
cd Terraform

terraform init
terraform validate
terraform plan
terraform apply
```

📷 **Screenshot:** Terraform Apply Output![alt text](TerraformAppply.png)

---

## Task 2 – Configuration Management using Ansible

After the EC2 instance was created, Ansible was used to configure the server automatically.

### Tasks Performed

* Connected to EC2 using SSH
* Installed Docker
* Pulled Docker Image
* Started Docker Container

### Command

```bash
ansible-playbook -i inventory playbook.yml
```

📷 **Screenshots:**

* Ansible Playbook
* Successful Playbook Execution

---

## Task 3 – Docker Containerization

The static website was containerized using Docker with the Nginx image.

### Build Docker Image

```bash
docker build -t elevance-cicd .
```

### Verify Image

```bash
docker images
```

### Run Container

```bash
docker run -d --name elevance-container -p 80:80 elevance-cicd
```

### Verify Container

```bash
docker ps
```

📷 **Screenshots:**

* Docker Build
* Docker Images
* Running Container

---

## Task 4 – Docker Compose

Docker Compose was included to simplify container deployment.

### Command

```bash
docker compose up -d
```

📷 **Screenshot:** Docker Compose Execution

---

## Task 5 – Jenkins CI/CD Pipeline

Jenkins was configured to automate the deployment process.

### Pipeline Stages

* Checkout Source Code
* Build Docker Image
* Verify Docker Image
* Deploy Docker Container

Whenever changes are pushed to GitHub, Jenkins builds and deploys the latest version of the project.

📷 **Screenshots:**

* Jenkins Dashboard
* Pipeline Configuration
* Successful Build
* Console Output

---

## Task 6 – GitHub Webhook

A GitHub Webhook was configured to trigger the Jenkins pipeline automatically after every push to the repository.

📷 **Screenshot:** GitHub Webhook Configuration

---

## Task 7 – Docker Hub

The Docker image was pushed to Docker Hub so that it could be pulled and deployed on the EC2 instance.

📷 **Screenshot:** Docker Hub Repository

---

## Deployment

After completing all the above tasks, the website was successfully deployed on an AWS EC2 instance and made accessible through its public IP address.

📷 **Screenshots:**

* EC2 Instance Running
* Live Website

---

## Challenges Faced

During the implementation of this project, I faced several challenges, including configuring Jenkins, writing Terraform scripts, setting up Ansible playbooks, and deploying Docker containers on AWS. These issues were resolved by referring to the official documentation of the respective tools and testing each component individually before integrating the complete workflow.

---

## Conclusion

This project helped me understand the complete DevOps workflow, from provisioning cloud infrastructure to automating application deployment. By integrating Terraform, Ansible, Docker, Jenkins, GitHub, and AWS, I gained practical experience in building a CI/CD pipeline and deploying applications in a cloud environment.

---

## Author

**Himanshu Sharma**

B.Tech Student

Elevance DevOps Internship

