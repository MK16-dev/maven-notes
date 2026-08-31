# Maven Project Structure

A Maven project follows a standard directory structure. This structure makes Maven projects easier to understand, build, and maintain.

---

## Standard Maven Project Structure

A basic Maven project looks like this:

    maven-demo/
    │
    ├── pom.xml
    │
    └── src/
        ├── main/
        │   ├── java/
        │   └── resources/
        │
        └── test/
            ├── java/
            └── resources/

---

## 1. `pom.xml`

`pom.xml` is the most important configuration file in a Maven project.

POM stands for:

**Project Object Model**

It contains information such as:

- Project details
- Dependencies
- Plugins
- Build configuration
- Project version
- Packaging type

Example:

    <groupId>com.example</groupId>
    <artifactId>maven-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

### Main Elements of `pom.xml`

| Element | Purpose |
|---|---|
| `groupId` | Identifies the project or organization |
| `artifactId` | Name of the project |
| `version` | Version of the project |
| `packaging` | Defines the package type such as JAR or WAR |
| `dependencies` | Defines libraries required by the project |
| `build` | Contains build configuration and plugins |

For example, our project uses Apache Commons Lang:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

Dependencies are added inside the `<dependencies>` section of `pom.xml`.

Maven reads `pom.xml` to understand the project, manage dependencies, run the build process, execute tests, and package the application.

---

## 2. `src/`

The `src` directory contains the source code and test code of the project.

It is divided into:

    src/
    ├── main/
    └── test/

---

## 3. `src/main/`

The `src/main` directory contains the main application code.

    src/main/
    ├── java/
    └── resources/

### `src/main/java/`

This directory contains the Java source code.

For example:

    src/main/java/com/example/App.java

The package structure is represented by folders:

    com/
    └── example/
        └── App.java

---

### `src/main/resources/`

This directory contains application resources required by the application.

Examples include:

- Configuration files
- Properties files
- XML files
- Other resource files

Example:

    src/main/resources/
    └── application.properties

If the project does not need any resources, this directory may not exist.

---

## 4. `src/test/`

The `src/test` directory contains code used for testing the application.

    src/test/
    ├── java/
    └── resources/

### `src/test/java/`

This directory contains test classes.

For example:

    src/test/java/com/example/AppTest.java

Our `maven-demo` project contains `AppTest.java`.

Maven compiles and executes this test when we run:

    mvn test

---

### `src/test/resources/`

This directory contains resources required specifically by tests.

For example:

    src/test/resources/
    └── test-data.properties

If the project does not require test resources, this directory may not exist.

---

# `target/`

Maven creates the `target` directory during the build process.

It contains generated build output.

For example:

    target/
    ├── classes/
    ├── test-classes/
    ├── surefire-reports/
    └── maven-demo-1.0-SNAPSHOT.jar

---

## `target/classes/`

Contains compiled application classes.

For example:

    target/classes/com/example/App.class

The `.java` source file is compiled into a `.class` file.

    App.java
       ↓
    Maven Compiler
       ↓
    App.class

---

## `target/test-classes/`

Contains compiled test classes.

For example:

    target/test-classes/com/example/AppTest.class

---

## `target/surefire-reports/`

The Maven Surefire Plugin creates test reports in this directory.

For example:

    target/surefire-reports/
    ├── com.example.AppTest.txt
    └── TEST-com.example.AppTest.xml

These files contain information about the tests that were executed.

---

## Generated JAR File

When we run:

    mvn package

Maven packages the application into a JAR file.

Our project generates:

    target/maven-demo-1.0-SNAPSHOT.jar

The general format is:

    artifactId-version.jar

So:

    maven-demo-1.0-SNAPSHOT.jar

contains:

    artifactId = maven-demo
    version    = 1.0-SNAPSHOT
    packaging  = jar

---

# Complete Maven Project Structure

After building the project, our structure can look like:

    maven-demo/
    │
    ├── pom.xml
    │
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   │   └── com/
    │   │   │       └── example/
    │   │   │           └── App.java
    │   │   │
    │   │   └── resources/
    │   │
    │   └── test/
    │       ├── java/
    │       │   └── com/
    │       │       └── example/
    │       │           └── AppTest.java
    │       │
    │       └── resources/
    │
    └── target/
        ├── classes/
        ├── test-classes/
        ├── surefire-reports/
        └── maven-demo-1.0-SNAPSHOT.jar

Some directories such as `resources`, `target`, and their contents may not exist until they are needed or generated by Maven.

---

# Important Difference

### Source Code

    src/main/java/

Contains the original Java source files.

### Compiled Code

    target/classes/

Contains compiled `.class` files.

### Test Code

    src/test/java/

Contains test source files.

### Compiled Test Code

    target/test-classes/

Contains compiled test classes.

### Build Output

    target/

Contains generated build files and artifacts.

---

# What Happens During a Maven Build?

For example:

    mvn package

Maven processes the project approximately like this:

    pom.xml
       ↓
    Read Project Configuration
       ↓
    Resolve Dependencies
       ↓
    Compile Source Code
       ↓
    Compile Test Code
       ↓
    Run Tests
       ↓
    Package Application
       ↓
    Create JAR
       ↓
    target/

---

# Key Points

- Maven follows a standard project structure.
- `pom.xml` is the main Maven configuration file.
- `src/main/java` contains application source code.
- `src/main/resources` contains application resources.
- `src/test/java` contains test source code.
- `src/test/resources` contains test resources.
- `target` contains generated build output.
- `target/classes` contains compiled application classes.
- `target/test-classes` contains compiled test classes.
- `target/surefire-reports` contains test reports.
- `mvn package` can create a JAR or WAR artifact.

---

# Quick Reference

| Directory/File | Purpose |
|---|---|
| `pom.xml` | Maven project configuration |
| `src/main/java` | Main Java source code |
| `src/main/resources` | Main application resources |
| `src/test/java` | Test source code |
| `src/test/resources` | Test resources |
| `target` | Generated build output |
| `target/classes` | Compiled application classes |
| `target/test-classes` | Compiled test classes |
| `target/surefire-reports` | Test reports |
| `target/*.jar` | Packaged JAR artifact |
