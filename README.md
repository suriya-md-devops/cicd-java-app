# End-to-End CI/CD pipeline for a Java Spring Boot application using Jenkins, Maven, SonarQube, Docker, Kubernetes, and Argo CD

<img width="1774" height="887" alt="image" src="https://github.com/user-attachments/assets/f34cb4e4-6fa6-4f86-bedc-0fb5527d227f" />

This project demonstrates automated application building, code analysis, Docker image creation, and GitOps-based deployment to Kubernetes.

## Tech Stack

- **Source Control:** Git, GitHub
- **CI/CD:** Jenkins
- **Build Tool:** Maven
- **Code Analysis:** SonarQube
- **Containerization:** Docker
- **Container Registry:** Docker Hub
- **Orchestration:** Kubernetes
- **GitOps:** Argo CD
- **Environment:** Linux / Ubuntu

## CI/CD Workflow

### Phase 1: Continuous Integration (CI)

**1. Source Code Checkout**
- Stored the Java application source code and Jenkinsfile in GitHub.
- Configured Jenkins using Pipeline Script from SCM to retrieve the Jenkinsfile from the repository.

**2. Custom Jenkins Agent**
- Created a custom Docker-based Jenkins agent image.
- Installed Java, Maven, Docker CLI, and Git.
- Configured Jenkins to execute pipeline stages inside the agent container.

**3. Build and Test**
- Used Maven to build and test the Java application.
- Generated the executable JAR file.

```bash
mvn clean package
```

**4. Static Code Analysis**
- Integrated SonarQube with Jenkins.
- Used the SonarQube Maven Scanner to analyze the Java source code.
- Configured authentication using Jenkins Credentials.
- Reviewed code quality and potential issues through the SonarQube dashboard.

**SonarQube Analysis Screenshot**

<img width="1900" height="735" alt="Screenshot 2026-11-11 151313" src="https://github.com/user-attachments/assets/4003f3fe-2467-4782-9c1a-fee5a31cc997" />

**5. Docker Image Build and Push**
- Created a Docker image for the Spring Boot application.
- Tagged images using Jenkins build numbers.
- Pushed the images to Docker Hub using Jenkins credentials.

```text
suriya2k5/ultimate-cicd:<BUILD_NUMBER>
```

**Jenkins Pipeline Screenshot**

<img width="1888" height="863" alt="Screenshot 2026-11-11 140946" src="https://github.com/user-attachments/assets/36dd6a58-f240-43f2-9476-6af731b88181" />

### Phase 2: Continuous Delivery (CD) – GitOps

**6. Kubernetes Manifest Update**
- Automated Docker image tag updates in the Kubernetes deployment manifest using a shell script and `sed`.
- Used Jenkins build numbers for image versioning.
- Committed and pushed updated manifests to GitHub.

**7. Argo CD Integration**
- Connected Argo CD to the GitHub repository containing Kubernetes manifests.
- Configured Argo CD to monitor the desired application state.
- Used Git as the single source of truth.
- Enabled synchronization between Git manifests and the Kubernetes cluster.

**Argo CD Dashboard Screenshot**

<img width="1916" height="871" alt="Screenshot 2026-11-11 140930" src="https://github.com/user-attachments/assets/35a1ee18-2c70-4c10-95ec-6f8bfc6d788a" />

**8. Kubernetes Deployment**
- Deployed the Java application to the Kubernetes cluster through Argo CD.
- Configured two application replicas in the deployment manifest.
- Kubernetes maintains the desired number of application pods.

## Key Highlights

- Implemented an end-to-end Jenkins CI/CD pipeline.
- Built a custom Docker-based Jenkins agent.
- Integrated Maven and SonarQube for building and code analysis.
- Automated Docker image creation and publishing.
- Automated Kubernetes manifest updates using shell scripting.
- Implemented GitOps-based deployment using Argo CD.
- Deployed the application on Kubernetes with two replicas.

## What I Learned

Gained practical experience with CI/CD automation, Jenkins pipeline configuration, Docker containerization, static code analysis, Kubernetes deployments, and GitOps workflows using Argo CD.
