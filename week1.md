# Introduction

 *Microservices* : An achitectural style wehre an application is broken down into small chunks of manageable services that communicate with each other and can be deployed independently 

 *DevOps* : Integrates Software Development and IT operations to shorten the SDLC and provide continous delivery

 *Continuous Integration (CI)* : Involves automatically testing and integrating new code changes into a shared repository several times a day.

 *Continuous Deployment (CD)* : Automates the deployment of code changes to a production environment

# DevOps Overview 

**DevOps** is defined as a set of practices, cultural philosophies, and tools that integrate software development and IT operations to deliver applications and services more rapidly and reliably

## *Introduction to CI/CD*

### What is CI/CD?
CI/CD stands for Continuous Integration and Continuous Deployment, a critical practice in modern software development. It involves the automatic building, testing, and deploying of applications to ensure that changes to the codebase are quickly integrated and deployed with minimal manual intervention.

### Continuous Integration (CI)
- **Code Repository**: When a user checks in code into a repository, it triggers an automated pipeline.
- **Pipeline Steps**:
  1. **Linting**: Ensuring code quality by checking for syntax errors. Although some organizations may skip this, it's a best practice to include it to catch any missed errors before the build stage.
  2. **Building**: This stage includes downloading necessary packages and can also include unit testing if configured to do so.
  3. **Unit Testing**: Involves testing individual parts or units of an application. To facilitate unit testing, a concept called 'mocking' is often used, especially when testing functions that rely on external calls.
  4. **SCA and SAST**: Software Compliance Analysis (SCA) and Static Analysis Security Testing (SAST) are crucial for ensuring that the code adheres to security standards and does not include known .


### Continuous Deployment (CD)

#### Deployment Pipeline
- **Artifacts Deployment**: The deployment begins from the artifact repository. It can be an independent pipeline or a continuation from CI.
- **System Integration Testing (SIT)**: This is the initial platform where the application is deployed for testing its interactions with other systems. It tests the application from a holistic perspective rather than in isolation.

# Linux Refresher

<ul>
  <li><strong>SSH connection:</strong> <code>ssh -i &lt;key.pem&gt; ubuntu@&lt;server-ip&gt;</code></li>

  <li><strong>Change directory:</strong> <code>cd ..</code></li>

  <li><strong>List directory contents:</strong> <code>ls</code></li>

  <li><strong>Show present working directory:</strong> <code>pwd</code></li>

  <li><strong>Change file permissions:</strong> <code>chmod 600 &lt;file&gt;</code></li>

  <li><strong>Copy file:</strong> <code>cp &lt;source&gt; &lt;destination&gt;</code></li>

  <li><strong>Create a new directory:</strong> <code>mkdir &lt;directory-name&gt;</code></li>

  <li>
    <strong>Install Docker using AWS CLI (not executed in class):</strong><br>
    <code>curl -fsSL https://get.docker.com -o get-docker.sh</code><br>
    <code>sudo sh get-docker.sh</code>
  </li>

  <li><strong>Check Docker version:</strong> <code>docker version</code></li>
</ul>
