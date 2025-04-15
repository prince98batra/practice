# 📋 SOP: Maven Common & Debugging Commands

**Owner:** Prince Batra  
**Team:** Downtime Crew  
**Date Created:** 14-Apr-2025  
**Last Updated:** 14-Apr-2025  

---

## 📦 Stack Details

- **Component:** Apache Maven  
- **Application Type:** Java (Maven Project)  
- **System:** Local (Ubuntu/Windows/Mac)  

---

## 🌟 Purpose

This SOP covers local Maven use for Java projects, including setup, common commands, and debugging steps — useful for building, testing, and troubleshooting.

---

## 🛠 Prerequisites (Local Setup)

### ✅ Step 1: Install Java (JDK 11 or higher)

**Ubuntu:**
```bash
sudo apt update
sudo apt install openjdk-17-jdk -y
java -version
```

**Mac:**
```bash
brew install openjdk@17
```

**Windows:**  
Download: [https://jdk.java.net](https://jdk.java.net)  
Set `JAVA_HOME` in environment variables.

---

### ✅ Step 2: Install Maven

**Ubuntu:**
```bash
sudo apt update
sudo apt install maven -y
mvn -v
```

**Mac:**
```bash
brew install maven
```

**Windows:**  
Download: [https://maven.apache.org/download.cgi](https://maven.apache.org/download.cgi)  
Set `MAVEN_HOME` in environment variables.

---

## 📂 Java Maven Project Structure

```
java/
├── pom.xml
└── src/
    └── main/
        └── java/
```

Navigate to project:
```bash
cd java
```

---

## 📘 What is Maven?

Maven is a build automation tool for Java. It manages:

- Compilation and packaging
- Dependencies
- Testing and reporting
- Deployment

All configurations are defined in `pom.xml` (Project Object Model).

---

## 🛠️ How Maven Works

When you run a Maven command, it goes through lifecycle phases:

- Code lives in `src/main/java`
- Tests in `src/test/java`
- Maven compiles, tests, and packages using `pom.xml`

---

## ✅ Commonly Used Maven Commands

### 1. **Clean compiled files**
```bash
mvn clean
```
**Expected Output:**
```
[INFO] Deleting /target
[INFO] BUILD SUCCESS
```
**Purpose:** Deletes `target/` directory  
**When to Use:** Before building fresh to avoid using old compiled files.

---

### 2. **Compile the project**
```bash
mvn compile
```
**Expected Output:**
```
[INFO] Compiling source to /target/classes
[INFO] BUILD SUCCESS
```
**Purpose:** Compiles `src/main/java` code  
**When to Use:** To verify syntax and compile code before packaging.

---

### 3. **Run unit tests**
```bash
mvn test
```
**Expected Output:**
```
[INFO] Running tests
[INFO] Tests run: X, Failures: 0
```
**Purpose:** Executes unit tests in `src/test/java`  
**When to Use:** To validate logic and ensure functionality.

---

### 4. **Create a JAR/WAR**
```bash
mvn package
```
**Expected Output:**
```
[INFO] Building jar: /target/project-name.jar
```
**Purpose:** Packages compiled code  
**When to Use:** When generating a deployable `.jar` or `.war`.

---

### 5. **Install the project locally**
```bash
mvn install
```
**Expected Output:**
```
[INFO] BUILD SUCCESS
```
**Purpose:** Installs build to local `.m2` repository  
**When to Use:** For local reuse or integration with other projects.

---

### 6. **Deploy the project**
```bash
mvn deploy
```
**Expected Output:**
```
[INFO] BUILD SUCCESS
```
**Purpose:** Pushes artifact to remote repo  
**When to Use:** When sharing builds across teams.

---

### 7. **Validate the project**
```bash
mvn validate
```
**Expected Output:**
```
[INFO] BUILD SUCCESS
```
**Purpose:** Verifies project structure and configs  
**When to Use:** Early in build to catch misconfigurations.

---

### 8. **Run integration tests**
```bash
mvn verify
```
**Expected Output:**
```
[INFO] BUILD SUCCESS
```
**Purpose:** Runs full test lifecycle  
**When to Use:** Before final deployment.

---

### 9. **Download all dependencies**
```bash
mvn dependency:resolve
```
**Expected Output:**
```
[INFO] Downloaded: junit:junit:4.13.2
```
**Purpose:** Downloads dependencies from `pom.xml`  
**When to Use:** On first-time setup or resolving missing libs.

---

### 10. **Print all dependencies**
```bash
mvn dependency:tree
```
**Expected Output:**
```
├─ junit:junit:4.13.2:test
```
**Purpose:** Displays full dependency hierarchy  
**When to Use:** Debug conflicts or inspect transitive dependencies.

---

### 11. **Clean and build**
```bash
mvn clean install
```
**Expected Output:**
```
[INFO] BUILD SUCCESS
```
**Purpose:** Clean, compile, test, and install  
**When to Use:** To perform a full local build.

---

### 12. **Skip tests**
```bash
mvn install -DskipTests
```
**Expected Output:**
```
[INFO] Tests are skipped.
```
**Purpose:** Builds without test execution  
**When to Use:** During dev cycles when tests aren't needed.

---

### 13. **Run specific test**
```bash
mvn -Dtest=ClassName test
```
**Expected Output:**
```
[INFO] Running com.example.ClassName
```
**Purpose:** Runs a specific test class or method  
**When to Use:** To isolate and debug a single test case.

---

## 😞 Debugging & Troubleshooting Commands

### 1. **Enable Debug Output**
```bash
mvn -X
```
**Purpose:** Shows verbose logs  
**When to Use:** When troubleshooting build failures.

---

### 2. **Print final POM**
```bash
mvn help:effective-pom
```
**Purpose:** Displays complete `pom.xml` with inherited config  
**When to Use:** To understand full build settings.

---

### 3. **Describe a plugin**
```bash
mvn help:describe -Dplugin=<plugin-name> -Ddetail
```
**Purpose:** Shows plugin version and usage  
**When to Use:** To debug plugin behavior or config.

---

### 4. **Force dependency update**
```bash
mvn clean install -U
```
**Purpose:** Updates local dependencies from remote  
**When to Use:** If local cache has outdated/missing files.

---

### 5. **Check Maven version**
```bash
mvn -v
```
**Purpose:** Shows Maven and Java versions  
**When to Use:** For verifying setup or compatibility.

---

### 6. **Show dependencies**
```bash
mvn dependency:resolve
```
**Purpose:** Resolves and downloads project dependencies  
**When to Use:** For setup or when facing missing jars.

---

### 7. **Clean and rebuild**
```bash
mvn clean install
```
**Purpose:** Performs fresh build  
**When to Use:** After major changes or cleanup.

---

### 8. **Show effective settings**
```bash
mvn help:effective-settings
```
**Purpose:** Displays active Maven settings  
**When to Use:** When dealing with profile/config issues.

---

### 9. **Run a specific test**
```bash
mvn -Dtest=ClassName test
```
**Purpose:** Re-run a single test class  
**When to Use:** For focused debugging.

---

## 🖚 End of SOP

| Date       | Author        | Change Description         |
|------------|---------------|----------------------------|
| 14-Apr-25  | Prince Batra  | Initial draft              |

---

