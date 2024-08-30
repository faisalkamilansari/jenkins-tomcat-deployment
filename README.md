# Jenkins Pipeline for Tomcat Deployment

This repository contains a Jenkins pipeline configuration for building, analyzing, and deploying a Maven-based Java application to Tomcat. The pipeline includes stages for code checkout, build, SonarQube analysis, and deployment to a Tomcat server.

## Prerequisites

- **Jenkins**: Ensure you have Jenkins installed and configured.
- **Maven**: Maven should be installed on the Jenkins agent where the build runs.
- **SonarQube**: A SonarQube server should be set up for code quality analysis.
- **Artifactory** (optional): An Artifactory server should be set up if you need to upload build artifacts.
- **Tomcat**: Tomcat server should be installed and configured on the target machine.

## Pipeline Configuration

### Pipeline Stages

1. **Checkout**
   - Clones the repository from GitHub.
   - Repository URL: `https://github.com/faisalkamilansari/jenkins-tomcat-deployment.git`
   - Branch: `main`

2. **Build**
   - Uses Maven to compile and package the application.
   - Maven Command: `mvn clean install`
   - Directory: `calc`

3. **SonarQube Analysis**
   - Analyzes the code using SonarQube.
   - Maven Command: `mvn clean verify sonar:sonar -Dsonar.projectKey=Jenkins-tomcat-deployment`
   - SonarQube Server ID: `SonarQube-Server`

4. **Deploy to Tomcat**
   - Deploys the WAR file to the Tomcat server.
   - Tomcat Service Name: `Tomcat9`
   - Tomcat Deployment Directory: `C:\\Program Files (x86)\\Apache Software Foundation\\Tomcat 9.0\\webapps`
   - WAR File Location: `C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Jenkins-tomcat-deployment\\calc\\target\\web-calculator.war`

### Pipeline Environment Variables

- **SONARQUBE_SERVER**: ID of the SonarQube server used for code analysis.
- **ARTIFACTORY_SERVER**: ID of the Artifactory server used for artifact upload (optional).

## Usage

1. **Configure Jenkins**
   - Set up Jenkins with the necessary plugins for Maven, SonarQube, and Artifactory.
   - Configure environment variables for SonarQube and Artifactory servers.

2. **Create a Pipeline Job**
   - Create a new pipeline job in Jenkins.
   - Copy the pipeline script from `Jenkinsfile` and paste it into the pipeline definition.

3. **Run the Pipeline**
   - Trigger the pipeline build in Jenkins.
   - Monitor the build and deployment process through the Jenkins interface.

4. **Verify Deployment**
   - Check the Tomcat server to ensure the WAR file has been deployed correctly.

## Post-Build Actions

- **Success**: Logs a success message upon successful build and deployment.
- **Failure**: Logs a failure message if the build or deployment fails.
- **Always**: Cleans up the workspace after the build.

## Troubleshooting

- Ensure all paths and server IDs are correctly configured in the pipeline script.
- Verify Maven and SonarQube installations and configurations on the Jenkins agent.
- Check Tomcat server logs for deployment issues.

---
