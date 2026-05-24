# Java Maven Jenkins Pipeline

A **production-ready Java Maven project** specifically designed for Jenkins CI/CD pipeline testing and demonstration. This project showcases best practices for Java development, Maven build automation, and Jenkins pipeline orchestration.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [System Requirements](#system-requirements)
- [Project Structure](#project-structure)
- [Quick Start](#quick-start)
- [Maven Build Commands](#maven-build-commands)
- [Running the Application](#running-the-application)
- [Unit Testing](#unit-testing)
- [Jenkins Pipeline Execution](#jenkins-pipeline-execution)
- [CI/CD Workflow](#cicd-workflow)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Project Overview

### Purpose
This project is a comprehensive example of a modern Java application configured for:
- ✅ **Java 21** - Latest LTS version with modern features
- ✅ **Maven** - Standard build automation tool
- ✅ **JUnit 5** - Latest testing framework
- ✅ **Jenkins** - Enterprise CI/CD pipeline automation
- ✅ **Production Ready** - Enterprise-grade configuration and best practices

### Key Features
- Complete Maven project structure with all required directories
- Fully functional `pom.xml` with Java 21 compiler configuration
- Sample application (`App.java`) with multiple utility methods
- Comprehensive unit tests using JUnit 5 (`AppTest.java`)
- Maven Surefire plugin for automated test execution
- Maven JAR plugin for creating executable artifacts
- Professional Jenkinsfile for pipeline automation
- Clean separation of concerns and documentation

---

## 📦 System Requirements

### Prerequisites
- **Java Development Kit (JDK) 21+**
  - Download: https://www.oracle.com/java/technologies/downloads/
  - Verify: `java -version`

- **Apache Maven 3.8.1+**
  - Download: https://maven.apache.org/download.cgi
  - Verify: `mvn -version`

- **Git**
  - Download: https://git-scm.com/downloads
  - Verify: `git --version`

### Optional Tools
- **Jenkins 2.0+** (for CI/CD pipeline execution)
- **Docker** (for containerized builds)
- **IDE/Editor** (IntelliJ IDEA, Eclipse, VS Code, etc.)

---

## 📁 Project Structure

```
Mavn-Project/
├── pom.xml                                   # Maven configuration file
├── Jenkinsfile                               # Declarative Jenkins pipeline
├── README.md                                 # This file
├── .gitignore                                # Git ignore rules
├── src/
│   ├── main/
│   │   └── java/
│   │       └── com/example/
│   │           └── App.java                  # Main application class
│   └── test/
│       └── java/
│           └── com/example/
│               └── AppTest.java              # Unit tests (JUnit 5)
└── target/                                   # Build output (generated)
    ├── classes/
    ├── test-classes/
    ├── surefire-reports/                     # Test reports
    └── *.jar                                 # Packaged JAR files
```

---

## 🚀 Quick Start

### 1. Clone the Repository
```bash
git clone https://github.com/NithishSGowda/Mavn-Project.git
cd Mavn-Project
```

### 2. Build the Project
```bash
mvn clean install
```

### 3. Run the Application
```bash
java -jar target/java-maven-jenkins-1.0.0.jar
```

### 4. Run Unit Tests
```bash
mvn test
```

---

## 🛠️ Maven Build Commands

### Complete Build Lifecycle

#### 1. **Clean** - Remove previous build artifacts
```bash
mvn clean
```
- Deletes the `target/` directory
- Use this before starting a fresh build
- Command: `mvn clean`

#### 2. **Compile** - Compile source code
```bash
mvn compile
```
- Compiles Java source files from `src/main/java/`
- Output placed in `target/classes/`
- Uses Java 21 compiler with strict linting enabled
- Command: `mvn compile`

#### 3. **Test** - Execute unit tests
```bash
mvn test
```
- Compiles test sources from `src/test/java/`
- Executes all `*Test.java` files using JUnit 5
- Generates test reports in `target/surefire-reports/`
- Fails the build if any test fails
- Command: `mvn test`

#### 4. **Package** - Create executable JAR
```bash
mvn package
```
- Executes clean, compile, and test phases
- Creates executable JAR: `target/java-maven-jenkins-1.0.0.jar`
- JAR includes manifest with main class entry
- Command: `mvn package`

#### 5. **Install** - Install to local Maven repository
```bash
mvn install
```
- Executes all previous phases including package
- Installs JAR to local Maven repository (~/.m2)
- Can be used as dependency in other projects
- Command: `mvn install`

### Combined Commands

#### Clean and Compile
```bash
mvn clean compile
```

#### Clean, Compile, and Test
```bash
mvn clean test
```

#### Full Build Pipeline
```bash
mvn clean install
```

#### Package Without Tests
```bash
mvn package -DskipTests
```

---

## 🎬 Running the Application

### Method 1: Direct JAR Execution
```bash
# Build first
mvn clean package

# Run the JAR
java -jar target/java-maven-jenkins-1.0.0.jar
```

### Method 2: Using Maven Exec Plugin
```bash
mvn exec:java -Dexec.mainClass="com.example.App"
```

### Expected Output
```
==========================================
Java Maven Jenkins Pipeline Demo
==========================================

Application Name: Java Maven Jenkins Pipeline
Application Version: 1.0.0
Java Version: 21.x.x
Build Time: username@os

Demonstration of utility methods:
Add 10 + 5 = 15
Multiply 6 * 7 = 42
Greet 'Jenkins' = Hello, Jenkins!

==========================================
Application execution completed successfully!
==========================================
```

---

## 🧪 Unit Testing

### Test Framework
- **JUnit 5 (Jupiter)** - Latest testing framework
- **Parameterized Tests** - Multiple test cases per method
- **Display Names** - Readable test output
- **Comprehensive Coverage** - All public methods tested

### Running Tests

#### Execute All Tests
```bash
mvn test
```

#### Run Specific Test Class
```bash
mvn test -Dtest=AppTest
```

#### Skip Tests During Build
```bash
mvn clean package -DskipTests
```

#### View Test Reports
```bash
# After running tests, view the report
ls -la target/surefire-reports/
```

### Test Coverage

The `AppTest.java` includes 24 comprehensive tests for:
- Arithmetic operations: `add()`, `multiply()`
- String operations: `greet()`, `isPalindrome()`
- Number validation: `isEven()`
- Metadata methods: `getApplicationName()`, `getApplicationVersion()`
- Edge cases and error handling

---

## 🔄 Jenkins Pipeline Execution

### Prerequisites for Jenkins Setup

1. **Install Jenkins Plugins**
   - Pipeline
   - Git
   - JUnit
   - Maven Integration

2. **Configure Tools in Jenkins**
   - Go to: Manage Jenkins → Configure System → Tool Locations
   - Configure Maven 3: Set name as `Maven-3`
   - Configure JDK: Set name as `JDK-21` pointing to Java 21

### Pipeline Stages

The Jenkinsfile defines 4 main stages:

```
┌─────────────────────────────────────────────┐
│         Jenkins Pipeline Execution          │
├─────────────────────────────────────────────┤
│ 1. Checkout   ✓ Clone repository            │
│ 2. Build      ✓ mvn clean compile           │
│ 3. Test       ✓ mvn test                    │
│ 4. Package    ✓ mvn package                 │
└─────────────────────────────────────────────┘
```

### Setting Up Jenkins Job

#### Step 1: Create New Pipeline Job
1. Click "New Item"
2. Enter job name: `JavaMavenPipeline`
3. Select "Pipeline"
4. Click OK

#### Step 2: Configure Pipeline
1. Under "Pipeline" section:
   - Select: "Pipeline script from SCM"
   - SCM: Git
   - Repository URL: `https://github.com/NithishSGowda/Mavn-Project.git`
   - Branch: `*/main`
   - Script Path: `Jenkinsfile`
2. Click Save

#### Step 3: Run the Job
1. Click "Build Now"
2. Monitor the build in real-time
3. View console output for details

---

## 🔌 CI/CD Workflow

### GitHub → Jenkins → Artifact

```
Developer Code → GitHub Push → Webhook
                                ↓
                         Jenkins Pipeline
                                ↓
                    Stage 1: Checkout
                    Stage 2: Build
                    Stage 3: Test
                    Stage 4: Package
                                ↓
                         JAR Artifact
```

---

## 🐛 Troubleshooting

### Issue 1: Maven Command Not Found
```bash
# Solution: Add Maven to PATH
export PATH=$PATH:/path/to/maven/bin
mvn -version
```

### Issue 2: Java 21 Not Found
```bash
# Solution: Set JAVA_HOME
export JAVA_HOME=/path/to/jdk-21
java -version
```

### Issue 3: Tests Failing Locally
```bash
# Run with verbose output
mvn test -X

# Run single test
mvn test -Dtest=AppTest#testAddPositiveIntegers
```

### Issue 4: Build Success but JAR not created
```bash
# Ensure package phase is executed
mvn clean package -DskipTests

# Verify JAR exists
ls -la target/*.jar
```

### Issue 5: Jenkins Pipeline Fails at Checkout
**Solution:**
1. Verify Jenkins has Git installed
2. Check GitHub credentials in Jenkins
3. Verify repository URL is correct
4. Check Jenkins logs: Build → Console Output

---

## 📊 Build Statistics

| Metric | Value |
|--------|-------|
| Java Version | 21 LTS |
| Maven Version | 3.8.1+ |
| Total Test Cases | 24 |
| Build Time | ~5-10 seconds |
| JAR Size | ~10 KB |
| Test Coverage | ~100% |

---

## ✅ Verification Checklist

After setup, verify everything is working:

- [ ] `mvn clean compile` - Compiles successfully
- [ ] `mvn test` - All 24 tests pass
- [ ] `mvn package` - JAR file created
- [ ] `java -jar target/java-maven-jenkins-1.0.0.jar` - Runs successfully
- [ ] Jenkins Jenkinsfile configured correctly
- [ ] All files in repository are committed
- [ ] `.gitignore` is working (target/ not tracked)

---

## 📚 Learning Resources

- **Maven Guide**: https://maven.apache.org/guides/getting-started/
- **JUnit 5 User Guide**: https://junit.org/junit5/docs/current/user-guide/
- **Jenkins Pipeline**: https://www.jenkins.io/doc/book/pipeline/
- **Java 21 Features**: https://www.oracle.com/java/technologies/javase/21-relnotes.html

---

## 📝 File Descriptions

| File | Purpose |
|------|---------|
| `pom.xml` | Maven configuration with Java 21, plugins, and JUnit 5 dependencies |
| `Jenkinsfile` | Declarative pipeline for Checkout, Build, Test, Package stages |
| `App.java` | Main application class with utility methods and demo entry point |
| `AppTest.java` | Comprehensive JUnit 5 unit tests with 24 test cases |
| `.gitignore` | Excludes build artifacts, IDE files, and logs from git |
| `README.md` | Complete project documentation and usage guide |

---

**Version**: 1.0.0  
**Status**: ✅ Production Ready  
**Last Updated**: 2026-05-24
