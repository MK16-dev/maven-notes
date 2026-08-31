# Essential Maven Commands

Maven commands are used to build, test, package, install, and manage Java projects.

The general syntax is:

```bash
mvn <phase>
```

---

## 1. Check Maven Version

```bash
mvn --version
```

Displays the installed Maven version, Java version, Maven home, and operating system information.

---

## 2. Clean the Project

```bash
mvn clean
```

Deletes the `target/` directory and removes previously generated build files.

---

## 3. Validate the Project

```bash
mvn validate
```

Checks whether the project structure and `pom.xml` are correct.

---

## 4. Compile the Project

```bash
mvn compile
```

Compiles the project's main Java source code.

Compiled files are placed inside:

```text
target/classes/
```

---

## 5. Run Tests

```bash
mvn test
```

Compiles the test code and runs the project's tests.

Test reports are generally generated under:

```text
target/surefire-reports/
```

---

## 6. Package the Project

```bash
mvn package
```

Compiles the project, runs tests, and creates the project artifact such as a `.jar` or `.war` file.

Example:

```text
target/
└── my-app-1.0.jar
```

---

## 7. Verify the Project

```bash
mvn verify
```

Runs the checks needed to verify that the project is valid and ready for installation or deployment.

---

## 8. Install the Artifact

```bash
mvn install
```

Builds the project and copies the generated artifact into the local Maven repository.

The default local repository is:

```text
~/.m2/repository/
```

On Windows:

```text
C:\Users\<username>\.m2\repository\
```

---

## 9. Deploy the Artifact

```bash
mvn deploy
```

Builds the project and uploads the artifact to a configured remote Maven repository.

This is commonly used in CI/CD pipelines.

---

# Common Command Combinations

### Clean and Package

```bash
mvn clean package
```

Removes the previous build and creates a fresh package.

### Clean and Install

```bash
mvn clean install
```

Cleans the project, builds it, runs tests, packages it, and installs the artifact into the local repository.

### Skip Tests

```bash
mvn package -DskipTests
```

Packages the application without running the tests.

> Note: Tests may still be compiled. If you want to skip both test compilation and execution, use `-Dmaven.test.skip=true`.

---

# Useful Maven Options

### `-D`

Defines a Maven property from the command line.

Example:

```bash
mvn package -DskipTests
```

### `-P`

Activates a Maven profile.

Example:

```bash
mvn package -Pdev
```

Profiles are covered separately in the Maven notes.

### `-e`

Displays detailed error information.

```bash
mvn package -e
```

### `-X`

Enables debug output.

```bash
mvn package -X
```

Useful when troubleshooting Maven problems.

---

# Dependency Tree

```bash
mvn dependency:tree
```

Displays the project's dependencies, including transitive dependencies.

Example:

```text
my-app
├── spring-core
│   └── ...
└── junit
```

This is useful for identifying dependency conflicts and understanding where a dependency comes from.

---

# Effective POM

```bash
mvn help:effective-pom
```

Displays the effective POM after Maven combines the project's POM with inherited settings, parent POM information, and other configuration.

Useful when you want to understand what Maven is actually using during the build.

---

# Maven Wrapper

Maven Wrapper allows a project to use a specific Maven version without requiring Maven to be installed globally.

### Linux / macOS

```bash
./mvnw clean package
```

### Windows

```cmd
mvnw.cmd clean package
```

The wrapper files are usually stored in:

```text
.mvn/
mvnw
mvnw.cmd
```

Using the wrapper is useful in team projects and CI/CD environments because everyone can use the Maven version defined by the project.

---

# Maven Command Flow

A typical Maven build can be represented as:

```text
mvn clean package
      ↓
Remove old build
      ↓
Compile source code
      ↓
Run tests
      ↓
Package application
      ↓
Create JAR / WAR
```

For a local Maven installation:

```bash
mvn clean package
```

For a project using Maven Wrapper:

```bash
./mvnw clean package
```

---

## Quick Reference

| Command                   | Purpose                              |
| ------------------------- | ------------------------------------ |
| `mvn --version`           | Check Maven version                  |
| `mvn clean`               | Remove `target/`                     |
| `mvn validate`            | Validate project                     |
| `mvn compile`             | Compile source code                  |
| `mvn test`                | Run tests                            |
| `mvn package`             | Create JAR/WAR                       |
| `mvn verify`              | Verify the build                     |
| `mvn install`             | Install artifact locally             |
| `mvn deploy`              | Upload artifact to remote repository |
| `mvn dependency:tree`     | Display dependency tree              |
| `mvn help:effective-pom`  | Display effective POM                |
| `mvn -e`                  | Show detailed errors                 |
| `mvn -X`                  | Enable debug output                  |
| `mvn package -DskipTests` | Package without running tests        |
| `mvn package -Pdev`       | Build using a profile                |

