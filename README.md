# Jenkins-Maven-build-008

This  demonstrates how to build a simple Java Maven application using **Jenkins Pipeline** inside **GitHub Codespaces**.






## 🧩 Project Overview

The goal of this task was to:

* Set up Jenkins in a GitHub Codespace environment.
* Configure Maven for Java build automation.
* Create a Jenkins pipeline (`Jenkinsfile`) that automatically builds the Java project using `mvn clean package`.

---

## ⚙️ Tools & Technologies

* **GitHub Codespaces** – Cloud-based development environment
* **Jenkins (LTS 2.479)** – Continuous Integration server
* **Maven 3.9.11** – Build automation tool
* **OpenJDK 11** – Java compiler/runtime
* **GitHub** – Source code management

---

## 🧠 Steps Performed

### 1. Created Java Maven Project

```bash
mkdir -p hello-java-maven/src/main/java
cd hello-java-maven
```

**HelloWorld.java**

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, Jenkins + Maven!");
    }
}
```

**pom.xml**

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>hello</artifactId>
  <version>1.0</version>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.1</version>
        <configuration>
          <source>11</source>
          <target>11</target>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

---

### 2. Installed Dependencies inside Codespace

```bash
sudo apt-get update -y
sudo apt-get install -y openjdk-11-jdk maven wget
```

---

### 3. Installed and Started Jenkins

```bash
wget -O jenkins.war https://get.jenkins.io/war/2.479/jenkins.war
java -jar jenkins.war --httpPort=8080
```

Accessed Jenkins from forwarded port `8080`, unlocked it using the initial password:

```bash
cat ~/.jenkins/secrets/initialAdminPassword
```

and installed **Suggested Plugins**.

---

### 4. Configured Jenkins Tools

* Added **Maven (maven3)** under *Manage Jenkins → Global Tool Configuration*.
* Verified Jenkins recognized Maven installation.

<img width="1096" height="585" alt="image" src="https://github.com/user-attachments/assets/d5754d1c-fea3-499c-961d-c09d8d7a5ff0" />



---

### 5. Created Jenkins Pipeline Job

**Jenkinsfile**

```groovy
pipeline {
  agent any
  tools { maven 'maven3' }
  stages {
    stage('Checkout') {
      steps { checkout scm }
    }
    stage('Build') {
      steps {
        dir('hello-java-maven') {
          sh 'mvn clean package'
        }
      }
    }
  }
}
```

<img width="1246" height="609" alt="image" src="https://github.com/user-attachments/assets/32215246-067f-4f16-8f16-25252c1e14e7" />
<img width="1278" height="575" alt="image" src="https://github.com/user-attachments/assets/7d698a07-70ba-4a6c-a294-51c02b15b079" />

---

### 6. Triggered Build

* Created a Pipeline job in Jenkins linked to this GitHub repository.
* Jenkins automatically cloned the repo and executed the pipeline stages.
* Build output displayed:

```
[INFO] BUILD SUCCESS
```
<img width="1238" height="531" alt="image" src="https://github.com/user-attachments/assets/69ae7c87-580a-470c-b266-c85aae97556d" />

---




## ✅ Result

* Jenkins successfully built the Java Maven project.
* Demonstrated end-to-end CI setup using Jenkins + Maven in Codespaces.

---

## 🏁 Outcome



* Setting up Jenkins from WAR file in Codespaces
* Configuring Maven builds in Jenkins
* Using Jenkinsfile for automated CI pipelines

---

**Author:** Rubeena Shaik

**Date:** November 2025
