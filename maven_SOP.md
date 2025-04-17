<p align="center">
  <img src="https://maven.apache.org/images/maven-logo-black-on-white.png" alt="Apache Maven Logo" width="250"/>
</p>


# SOP: Maven Common & Debugging Commands

## 👤 **Author Information**
| **Author** | **Created on** | **Version**  | **Comment** | **Reviewer** |
|------------|----------------|--------------|-------------|--------------|
| **Prince Batra**   | **14-04-2025**   | **Version 1** | **Internal review** | **Siddharth Pawar** |
| **Prince Batra**   | **14-04-2025**   | **Version 1.1** | **L0 review** | **Shikha** |

---

## 📑 Table of Contents

1. [Introduction](#1-introduction)  
2. [What is Maven?](#2-what-is-maven)  
3. [Why Use Maven?](#3-why-use-maven)  
4. [How Maven Works](#4-how-maven-works)  
5. [Example Project Structure](#5-example-java-maven-project-structure)  
6. [Prerequisites (Install Maven)](#6-prerequisites-install-on-local-system)  
7. [Commonly Used Maven Commands](#7-commonly-used-maven-commands)
8. [Debugging & Troubleshooting Commands](#8-debugging--troubleshooting-commands) 
9. [Contact Information](#contact-information)
10. [References](#references)


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

## **7. Commonly Used Maven Commands**

---

| **Task** | **Command** | **Expected Output** | **Purpose** | **When to Use** |
|------|-------------|---------------------|-------------|-----------------|
| 1. **Clean compiled files** | `mvn clean` | ```[INFO] Deleting /path/to/project/target```<br>```[INFO] BUILD SUCCESS``` | Removes the `target/` directory with old build files. | Before a fresh build to ensure no leftover files affect the process. |
| 2. **Compile the project** | `mvn compile` | ```[INFO] Compiling 1 source file to /path/to/project/target/classes```<br>```[INFO] BUILD SUCCESS``` | Converts source code into bytecode. | To check for compilation errors before testing or packaging. |
| 3. **Run unit tests** | `mvn test` | ```[INFO] Running com.example.projectname.TestClass```<br>```[INFO] Tests run: 5, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.012 sec```<br>```[INFO] BUILD SUCCESS``` | Runs test cases from `src/test/java` using test frameworks. | To verify if individual components are working correctly. |
| 4. **Create a JAR/WAR** | `mvn package` | ```[INFO] Building jar: /path/to/project/target/project-name-1.0-SNAPSHOT.jar```<br>```[INFO] BUILD SUCCESS``` | Packages compiled code into deployable artifacts like `.jar` or `.war`. | When preparing the application for deployment or delivery. |
| 5. **Install the Project Locally** | `mvn install` | ```[INFO] BUILD SUCCESS``` | Installs built artifact into your local Maven repository. | When you want the project available locally for use in other projects. |
| 6. **Deploying the Project** | `mvn deploy` | ```[INFO] BUILD SUCCESS``` | Uploads the artifact to a remote Maven repository. | When sharing the project with teams or external applications. |
| 7. **Validate the Project** | `mvn validate` | ```[INFO] BUILD SUCCESS``` | Verifies if project structure and dependencies are correctly set. | For checking proper project setup before proceeding. |
| 8. **Run integration tests** | `mvn verify` | ```[INFO] BUILD SUCCESS``` | Runs full test lifecycle including integration tests. | To ensure the system works as a whole before deployment. |
| 9. **Download all dependencies** | `mvn dependency:resolve` | ```[INFO] Downloaded: junit:junit:4.13.2```<br>```[INFO] BUILD SUCCESS``` | Fetches all libraries defined in `pom.xml`. | During initial setup or when dependencies fail to resolve. |
| 10. **Print all dependencies** | `mvn dependency:tree` | ```com.example.projectname:project-name:jar:1.0-SNAPSHOT```<br>```├── junit:junit:jar:4.13.2:test```<br>```└── org.springframework:spring-core:jar:5.3.8``` | Shows a tree of direct and transitive dependencies. | To inspect or debug library conflicts and structure. |
| 11. **Clean and build the project** | `mvn clean install` | ```[INFO] BUILD SUCCESS``` | Cleans old builds, compiles code, runs tests, installs locally. | For a full clean rebuild and local installation. |
| 12. **Skip tests during build** | `mvn install -DskipTests` | ```[INFO] Tests are skipped.```<br>```[INFO] BUILD SUCCESS``` | Builds and installs without running tests. | During quick development cycles (avoid for production builds). |
| 13. **Run a specific test** | `mvn -Dtest=ClassName test` | ```[INFO] Running com.example.projectname.TestClass```<br>```[INFO] Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 0.005 sec```<br>```[INFO] BUILD SUCCESS``` | Runs only a specified test class or method. | When focusing on or debugging a particular test. |

---

## **8. Debugging & Troubleshooting Commands**

| **#** | **Command** | **Expected Output** | **Purpose** | **When to Use** |
|------|-------------|---------------------|-------------|-----------------|
| 1. **Enable Debugging Output** | ```bash<br>mvn -X<br>``` | ```bash<br>[DEBUG] [INFO] --- maven-clean-plugin:3.1.0:clean (default-clean) @ project-name ---<br>[DEBUG] [INFO] BUILD SUCCESS<br>``` | Shows detailed logs for the entire build process. | When builds fail and you need more context for debugging. |
| 2. **Print the Final POM (Project Configuration)** | ```bash<br>mvn help:effective-pom<br>``` | ```bash<br>[INFO] Scanning for projects...<br>[INFO] Effective POM for project project-name: 1.0-SNAPSHOT<br>``` | Shows complete effective project configuration. | To view all applied POM settings including inherited ones. |
| 3. **Show Information About a Plugin** | ```bash<br>mvn help:describe -Dplugin=<plugin-name> -Ddetail<br>``` | ```bash<br>[INFO] Describing plugin org.apache.maven.plugins:maven-clean-plugin:3.1.0<br>``` | Describes usage, goals, and config of a specific plugin. | When understanding or troubleshooting Maven plugins. |
| 4. **Force Maven to Update Dependencies** | ```bash<br>mvn clean install -U<br>``` | ```bash<br>[INFO] BUILD SUCCESS<br>``` | Downloads the latest versions of dependencies, even if already cached locally. | When your project uses outdated libraries or new versions are not picked up |
| 5. **Check Your Maven Version** | ```bash<br>mvn -v<br>``` | ```bash<br>Apache Maven 3.6.3<br>Maven home: /path/to/maven<br>Java version: 1.8.0_252, vendor: Oracle Corporation<br>``` | Shows your Maven and Java versions. | To confirm installed versions or check compatibility issues. |
| 6. **Show Effective Settings** | ```bash<br>mvn help:effective-settings<br>``` | ```bash<br>[INFO] Effective settings for Maven<br>``` | Displays the final settings Maven uses (default + custom). | For debugging settings or verifying profile configurations. |

---

## **Contact Information**
| **Name** | **Email Address**        |
|----------|--------------------------|
| **Prince Batra**  | **prince.batra.snaatak@mygurukulam.co**   |

---

## **References**

| **Links** | **Overview** |
|-----------|--------------|
| [Official Apache Maven Documentation](https://maven.apache.org/guides/index.html) | Central hub for all official Maven guides and documentation. |
| [Maven Lifecycle Reference](https://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html) | Explains Maven's build lifecycle phases and how they are structured. |
| [Maven Plugin Documentation](https://maven.apache.org/plugins/) | Index of official Maven plugins with usage details and configuration options. |
| [Effective POM and Settings](https://maven.apache.org/configure.html) | Covers configuration management via `pom.xml` and `settings.xml`. |

---
