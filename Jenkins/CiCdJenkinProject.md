# CI/CD Pipeline – Jenkins, Maven, SonarQube, Docker, ECR, ECS

## Introduction
This project implements a complete Continuous Integration and Continuous Deployment (CI/CD) pipeline using Jenkins. The goal is to automatically build, test, analyze, package, containerize, and deploy the Vprofile application into Amazon ECS.

The pipeline follows an industry-standard workflow commonly used in real DevOps environments.

---

## Project Overview
The CI/CD flow used in this project:

Developer → GitHub → Jenkins → Maven Build → Unit Test → Checkstyle → SonarQube → Quality Gate → Docker Build → Push to ECR → Deploy to ECS

This automation ensures:
- Every code change is tested and analyzed
- Code quality remains consistent
- Docker images are versioned properly
- Deployments to ECS happen automatically

---

## Tools Used

### Jenkins
Acts as the automation server responsible for running each stage of the pipeline.

### GitHub
Stores the project source code.

### Maven
Used for application build, unit testing, and checkstyle validation.

### SonarQube
Performs static code analysis and ensures quality standards through the Quality Gate.

### Docker
Packages the application into a container image using a multistage Dockerfile.

### Amazon ECR
Stores the generated Docker images.

### Amazon ECS
Runs the containerized application as a service inside a cluster.

---

## Pipeline Architecture
The pipeline is built using Jenkinsfile (Pipeline as Code).  
Stages included:

1. **Fetch Code**
   - Jenkins clones the GitHub repository.

2. **Build**
   - Maven compiles and packages the application.
   - The .war file is archived for reference.

3. **Unit Test**
   - Maven runs unit tests to validate functionality.

4. **Checkstyle Analysis**
   - Code style and formatting issues are checked.

5. **SonarQube Code Analysis**
   - Complete static code analysis is performed.
   - Issues such as bugs, vulnerabilities, and code smells are reported.

6. **Quality Gate**
   - Ensures the code meets required standards before moving forward.

7. **Docker Image Build**
   - Jenkins builds the container image from the application's Dockerfile.
   - Each image is tagged with the Jenkins build number.

8. **Push Image to AWS ECR**
   - The Docker image is pushed to ECR.
   - Two tags are pushed:
     - Build number (versioned)
     - Latest

9. **Remove Local Images**
   - Old Docker images are removed from the Jenkins agent to free space.

10. **Deploy to Amazon ECS**
   - ECS service is updated using “force new deployment”.
   - ECS pulls the new image from ECR and deploys it.

---

## Environment Variables Used
The pipeline uses Jenkins environment variables such as:

- AWS credentials ID  
- ECR registry URL  
- ECS cluster name  
- ECS service name  
- Maven version  
- JDK version  
- Docker registry URL  

These are configured in Jenkins to keep the pipeline dynamic and reusable.

---

## How Deployment Works in ECS
- The ECS service monitors the container image stored in ECR.
- When Jenkins triggers a new deployment:
  - ECS pulls the new image version.
  - A rolling update happens:
    - New tasks start
    - Old tasks stop only after new ones become healthy
- This ensures zero downtime deployment.

---

## Project Flow Summary
1. Code is pushed to GitHub.  
2. Jenkins fetches the code.  
3. Maven builds the project, runs tests, and performs checkstyle.  
4. SonarQube analyzes the code.  
5. If quality gate passes, a Docker image is built.  
6. The image is pushed to Amazon ECR.  
7. Jenkins triggers a new deployment in Amazon ECS.  
8. ECS updates the service using the new image.  

---

## Benefits of This Pipeline
- Fully automated CI/CD flow  
- Ensures high code quality  
- Eliminates manual deployment steps  
- Provides version-controlled Docker images  
- Achieves fast, reliable, repeatable deployments  
- Fits industry DevOps standards  

---

## Conclusion
This project demonstrates a complete CI/CD pipeline that integrates code building, testing, analysis, containerization, and cloud deployment. It showcases how DevOps teams automate delivery processes using Jenkins, Docker, and AWS services such as ECR and ECS.

The Jenkinsfile used for this project is placed in the repository and contains the full pipeline logic.


