* Jenkins + Docker setup on EC2
* `my-first-pipeline` project
* `multi-stage-multi-agent` project

---

### 📄 Cleaned `README.md`

````markdown
# Jenkins CI/CD Hands-on – My Projects

This repository showcases Jenkins pipeline projects using Docker as build agents. All hands-on work is done on an EC2 instance with Jenkins and Docker installed.

---

## 🧱 Environment Setup

- **Jenkins installed** on Ubuntu EC2 instance.
- **Docker installed** on the same machine.
- Jenkins exposed via port `8080` in EC2 security group.
- Installed **Docker Pipeline Plugin** via Jenkins Plugin Manager.
- Restarted Jenkins after plugin installation.

---

## 📦 Project 1: `my-first-pipeline`

### 📝 Objective

Run a simple Jenkins pipeline using a Docker image (`python:3.9`) as the agent.

### 🔧 Jenkinsfile

```groovy
pipeline {
  agent {
    docker { image 'python:3.9' }
  }
  stages {
    stage('Build') {
      steps {
        sh 'python --version'
      }
    }
  }
}
````

### ✅ Outcome

* Jenkins pulled and used `python:3.9` container.
* Printed Python version.
* Verified Docker agent functionality.

---

## 📦 Project 2: `multi-stage-multi-agent`

### 📝 Objective

Create a multi-stage pipeline where each stage uses a different Docker image, simulating backend, frontend, and DB components.

### 🔧 Jenkinsfile

```groovy
pipeline {
  agent none
  stages {
    stage('Backend') {
      agent { docker { image 'maven:3.8.1' } }
      steps {
        sh 'mvn --version'
      }
    }
    stage('Frontend') {
      agent { docker { image 'node:16-alpine' } }
      steps {
        sh 'node --version'
      }
    }
    stage('Database') {
      agent { docker { image 'mysql:latest' } }
      steps {
        sh 'echo "SELECT * FROM xyz;"'
      }
    }
  }
}
```

### ✅ Outcome

* Each stage ran in its own container:

  * Maven for backend
  * Node.js for frontend
  * MySQL for DB
* Showcased isolated execution using multiple agents.

---

## 📌 Key Concepts

* Use of `docker` directive for per-stage agents.
* `agent none` disables default agent, enabling custom container per stage.
* Each container runs independently and is removed after execution.

---

