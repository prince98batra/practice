<p align="center">
  <img src="https://maven.apache.org/images/maven-logo-black-on-white.png" alt="Apache Maven Logo" width="250"/>
</p>


# SOP: Maven Common & Debugging Commands

## 👤 **Author Information**
| **Author** | **Created on** | **Version**  | **Comment** | **Reviewer** |
|------------|----------------|--------------|-------------|--------------|
| **Prince Batra**   | **14-04-2025**   | **Version 1** | **Internal review** | **Siddharth Pawar** |
---

## 📑 Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Maven?](#2-what-is-maven)  
3. [Why Use Maven?](#3-why-use-maven)  
4. [How Maven Works](#4-how-maven-works)  
5. [Example Project Structure](#5-example-java-maven-project-structure)  
6. [Prerequisites (Install Maven)](#6-prerequisites-install-on-local-system)  
7. [Commonly Used Maven Commands](#7-commonly-used-maven-commands)
   - [1. Clean compiled files](#1-clean-compiled-files)
   - [2. Compile the project](#2-compile-the-project)
   - [3. Run unit tests](#3-run-unit-tests)
   - [4. Create a JAR/WAR](#4-create-a-jarwar)
   - [5. Install the Project Locally](#5-install-the-project-locally)
   - [6. Deploying the Project](#6-deploying-the-project)
   - [7. Validate the Project](#7-validate-the-project)
   - [8. Run integration tests](#8-run-integration-tests)
   - [9. Download all dependencies](#9-download-all-dependencies)
   - [10. Print all dependencies](#10-print-all-dependencies)
   - [11. Clean and build the project](#11-clean-and-build-the-project)
   - [12. Skip tests during build](#12-skip-tests-during-build)
   - [13. Run a specific test](#13-run-a-specific-test)
8. [Debugging & Troubleshooting Commands](#8-debugging--troubleshooting-commands)  
   - [1. Enable Debugging Output](#1-enable-debugging-output)
   - [2. Print the Final POM (Project Configuration)](#2-print-the-final-pom-project-configuration)
   - [3. Show Information About a Plugin](#3-show-information-about-a-plugin)
   - [4. Force Maven to Update Dependencies](#4-force-maven-to-update-dependencies)
   - [5. Check Your Maven Version](#5-check-your-maven-version)
   - [6. Show Effective Settings](#6-show-effective-settings)
9. [References](#9-references)
10. [Contact Information](#contact-information)


---

## 1. Introduction

This SOP provides a quick reference to the most commonly used Maven commands and debugging techniques for Java developers. It is meant to simplify daily development tasks such as building, testing, and troubleshooting Maven-based projects in local environments.

---

## 2. What is Maven?

- Maven is a build automation tool designed for Java projects.  
- It helps manage project builds, reporting, documentation, and dependencies.  
- A central configuration file `pom.xml` manages all settings.

---

## 3. Why Use Maven?

- Simplifies project structure and build lifecycle.  
- Automatically downloads dependencies.  
- Supports testing, packaging, and deployment in a standardized way.  
- Makes team collaboration easier with consistent builds.

---

## 4. How Maven Works

- Maven follows a build lifecycle with phases like **validate → compile → test → package → verify → install → deploy**.  
- All configuration lies in the `pom.xml` file.  
- Code lives inside `src/main/java`, and test files inside `src/test/java`.

---

## 5. Example Java Maven Project Structure

```bash
java/
├── pom.xml                     # Project Object Model file (Maven's config file)
└── src/                        # Source folder (contains all project code)
    └── main/                   # Main application code (not tests)
        └── java/               # Java source files go here (e.g., .java classes)
```

---

## 6. Prerequisites (Install on Local System)

### ✅ Step 1: Install Java (JDK 11 or higher)

**Ubuntu:**
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```
---

### ✅ Step 2: Install Maven

**Ubuntu:**
```bash
sudo apt update
sudo apt install maven -y
mvn -v
```

---

## ✅ **7. Commonly Used Maven Commands**

---

### 1. **Clean compiled files**

- **Command:** 

```
mvn clean
```
Expected Output
```
[INFO] Deleting /path/to/project/target
[INFO] BUILD SUCCESS
```

- **Purpose:** Removes the `target/` directory with old build files.  
- **When to Use:** Before a fresh build to ensure no leftover files affect the process.

---

### 2. **Compile the project**

- **Command:** 

```
mvn compile
```  
Expected Output
```
[INFO] Compiling 1 source file to /path/to/project/target/classes
[INFO] BUILD SUCCESS
```

- **Purpose:** Converts source code into bytecode.  
- **When to Use:** To check for compilation errors before testing or packaging.

---

### 3. **Run unit tests**

- **Command:** 
```
mvn test
```  
Expected Output
```
[INFO] Running com.example.projectname.TestClass
[INFO] Tests run: 5, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.012 sec
[INFO] BUILD SUCCESS
```

- **Purpose:** Runs test cases from `src/test/java` using test frameworks.  
- **When to Use:** To verify if individual components are working correctly.

---

### 4. **Create a JAR/WAR**

- **Command:** 

```
mvn package
```
Expected Output
```
[INFO] Building jar: /path/to/project/target/project-name-1.0-SNAPSHOT.jar
[INFO] BUILD SUCCESS
```

- **Purpose:** Packages compiled code into deployable artifacts like `.jar` or `.war`.  
- **When to Use:** When preparing the application for deployment or delivery.

---

### 5. **Install the Project Locally**

- **Command:**
```
mvn install
```
Expected Output
```
[INFO] BUILD SUCCESS
```

- **Purpose:** Installs built artifact into your local Maven repository.  
- **When to Use:** When you want the project available locally for use in other projects.

---

### 6. **Deploying the Project**

- **Command:**
```
mvn deploy
```
Expected Output
```
[INFO] BUILD SUCCESS
```

- **Purpose:** Uploads the artifact to a remote Maven repository.  
- **When to Use:** When sharing the project with teams or external applications.

---

### 7. **Validate the Project**

- **Command:**
```
mvn validate
```
Expected Output
```
[INFO] BUILD SUCCESS
```

- **Purpose:** Verifies if project structure and dependencies are correctly set.  
- **When to Use:** For checking proper project setup before proceeding.

---

### 8. **Run integration tests**

- **Command:** 
```
mvn verify
```  
Expected Output
```
[INFO] BUILD SUCCESS
```
- **Purpose:** Runs full test lifecycle including integration tests.  
- **When to Use:** To ensure the system works as a whole before deployment.

---

### 9. **Download all dependencies**

- **Command:** 
```
mvn dependency:resolve 
``` 
Expected Output
```
[INFO] Downloaded: junit:junit:4.13.2
[INFO] BUILD SUCCESS
```

- **Purpose:** Fetches all libraries defined in `pom.xml`.  
- **When to Use:** During initial setup or when dependencies fail to resolve.

---

### 10. **Print all dependencies**

- **Command:**
```
mvn dependency:tree
```
Expected Output
```
com.example.projectname:project-name:jar:1.0-SNAPSHOT
├── junit:junit:jar:4.13.2:test
└── org.springframework:spring-core:jar:5.3.8
```
- **Purpose:** Shows a tree of direct and transitive dependencies.  
- **When to Use:** To inspect or debug library conflicts and structure.

---

### 11. **Clean and build the project**

- **Command:** 
```
mvn clean install
```
Expected Output
```
[INFO] BUILD SUCCESS
```
- **Purpose:** Cleans old builds, compiles code, runs tests, installs locally.  
- **When to Use:** For a full clean rebuild and local installation.

---

### 12. **Skip tests during build**

- **Command:** 
```
mvn install -DskipTests
```
Expected Output
```
[INFO] Tests are skipped.
[INFO] BUILD SUCCESS
```
- **Purpose:** Builds and installs without running tests.  
- **When to Use:** During quick development cycles (avoid for production builds).

---

### 13. **Run a specific test**

- **Command:** 
```
mvn -Dtest=ClassName test
```  
Expected Output
```
[INFO] Running com.example.projectname.TestClass
[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.005 sec
[INFO] BUILD SUCCESS
```
- **Purpose:** Runs only a specified test class or method.  
- **When to Use:** When focusing on or debugging a particular test.

---


## 8. Debugging & Troubleshooting Commands


### 1. **Enable Debugging Output**

- **Command:**  
  ```bash
  mvn -X
  ```

- **Expected Output:**  
  ```bash
  [DEBUG] [INFO] --- maven-clean-plugin:3.1.0:clean (default-clean) @ project-name ---
  [DEBUG] [INFO] BUILD SUCCESS
  ```

- **Purpose:** Shows detailed logs for the entire build process.  
- **When to Use:** When builds fail and you need more context for debugging.

---

### 2. **Print the Final POM (Project Configuration)**

- **Command:**  
  ```bash
  mvn help:effective-pom
  ```

- **Expected Output:**  
  ```bash
  [INFO] Scanning for projects...
  [INFO] Effective POM for project project-name: 1.0-SNAPSHOT
  ```

- **Purpose:** Shows complete effective project configuration.  
- **When to Use:** To view all applied POM settings including inherited ones.

---

### 3. **Show Information About a Plugin**

- **Command:**  
  ```bash
  mvn help:describe -Dplugin=<plugin-name> -Ddetail
  ```

- **Expected Output:**  
  ```bash
  [INFO] Describing plugin org.apache.maven.plugins:maven-clean-plugin:3.1.0
  ```

- **Purpose:** Describes usage, goals, and config of a specific plugin.  
- **When to Use:** When understanding or troubleshooting Maven plugins.

---

### 4. **Force Maven to Update Dependencies**

- **Command:**  
  ```bash
  mvn clean install -U
  ```

- **Expected Output:**  
  ```bash
  [INFO] BUILD SUCCESS
  ```

- **Purpose:**  Downloads the latest versions of dependencies, even if already cached locally.

- **When to Use:**  When your project uses outdated libraries or new versions are not picked up
  
---

### 5. **Check Your Maven Version**

- **Command:**  
  ```bash
  mvn -v
  ```

- **Expected Output:**  
  ```bash
  Apache Maven 3.6.3
  Maven home: /path/to/maven
  Java version: 1.8.0_252, vendor: Oracle Corporation
  ```

- **Purpose:**  Shows your Maven and Java versions.

- **When to Use:**  To confirm installed versions or check compatibility issues.

---

### 6. **Show Effective Settings**

- **Command:**  
  ```bash
  mvn help:effective-settings
  ```

- **Expected Output:**  
  ```bash
  [INFO] Effective settings for Maven
  ```

- **Purpose:**  Displays the final settings Maven uses (default + custom).

- **When to Use:**  For debugging settings or verifying profile configurations.

---

## 9. References

- [Official Apache Maven Documentation](https://maven.apache.org/guides/index.html)  
- [Maven Lifecycle Reference](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)  
- [Maven Plugin Documentation](https://maven.apache.org/plugins/)  
- [Effective POM and Settings](https://maven.apache.org/configure.html)

---

## 📬 **Contact Information**
| **Name** | **Email Address**        |
|----------|--------------------------|
| **Prince Batra**  | **prince.batra.snaatak@mygurukulam.co**   |

