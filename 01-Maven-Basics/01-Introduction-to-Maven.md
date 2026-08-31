# What is Maven?

Maven is a build automation and project management tool mainly used for Java projects.

It helps developers manage a project's:

- Build process
- Dependencies
- Testing
- Packaging
- Plugins
- Project configuration

Maven follows a standard project structure and uses a file called `pom.xml` to manage the project.

---

## Why Do We Use Maven?

Without Maven, developers may have to manually:

- Download required JAR files
- Add JAR files to the project
- Manage different library versions
- Compile source code
- Run tests
- Package the application

Maven automates most of these tasks.

---

## Maven as a Build Automation Tool

Maven can automate common tasks involved in building a Java application.

For example:

    Compile
       ↓
    Test
       ↓
    Package
       ↓
    Install

Instead of performing each step manually, Maven can execute these steps using Maven commands.

---

## Maven as a Dependency Management Tool

A Java application often requires external libraries.

For example, our `maven-demo` project uses:

    Apache Commons Lang

Instead of downloading the JAR manually, we add the dependency to `pom.xml`.

Example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

Maven downloads the required library and makes it available to the project.

---

## Maven Central Repository

Maven can download dependencies from repositories.

The most commonly used public repository is:

    Maven Central Repository

For example, when Maven downloaded dependencies during our project build, we saw:

    Downloading from central:
    https://repo.maven.apache.org/maven2/

Maven searches the configured repositories for the required dependencies.

---

## Local Maven Repository

Maven also maintains a local repository on the developer's computer.

On Windows, it is normally located at:

    C:\Users\<username>\.m2\repository

For our system:

    C:\Users\mital\.m2\repository

Downloaded dependencies are stored there so Maven can reuse them in future builds.

This avoids downloading the same dependency again if it is already available locally.

---

## Maven and `pom.xml`

Every Maven project normally has a `pom.xml` file.

POM stands for:

    Project Object Model

The `pom.xml` file contains important project information such as:

- Group ID
- Artifact ID
- Version
- Packaging
- Dependencies
- Plugins
- Build configuration

Example:

    <groupId>com.example</groupId>
    <artifactId>maven-demo</artifactId>
    <version>1.0-SNAPSHOT</version>
    <packaging>jar</packaging>

---

## Maven Coordinates

Maven identifies an artifact using coordinates.

The main coordinates are:

    groupId
    artifactId
    version

Example:

    groupId    = com.example
    artifactId = maven-demo
    version    = 1.0-SNAPSHOT

These values uniquely identify a particular version of a Maven project or artifact.

---

## Maven Artifact

An artifact is a file produced or managed by Maven.

For example, when we ran:

    mvn package

our project produced:

    maven-demo-1.0-SNAPSHOT.jar

This JAR is the packaged artifact of our Maven project.

---

## Maven Build Process

A typical Maven build can involve:

    pom.xml
       ↓
    Read project configuration
       ↓
    Resolve dependencies
       ↓
    Compile source code
       ↓
    Compile test code
       ↓
    Run tests
       ↓
    Package application
       ↓
    Generate artifact

Maven controls this process using its build lifecycle.

---

## Example: Our `maven-demo` Project

Our Maven project contains:

    maven-demo/
    ├── pom.xml
    └── src/

The `pom.xml` contains the project configuration and dependencies.

We used Maven commands such as:

    mvn compile

    mvn test

    mvn package

    mvn install

These commands allowed Maven to compile, test, package, and install our project.

---

## Advantages of Maven

### 1. Dependency Management

Automatically downloads and manages required libraries.

### 2. Build Automation

Automates compilation, testing, packaging, and other build tasks.

### 3. Standard Project Structure

Provides a consistent structure for Maven projects.

### 4. Reusable Configuration

The `pom.xml` stores project configuration in one place.

### 5. Plugin Support

Maven provides plugins for compiling, testing, packaging, and many other tasks.

### 6. Repository Support

Maven can download dependencies from repositories such as Maven Central.

### 7. Consistent Builds

Developers can use the same Maven configuration to build the project consistently.

---

## Maven vs Manual JAR Management

| Manual JAR Management | Maven |
|---|---|
| Download JAR files manually | Maven downloads dependencies |
| Add JARs manually | Dependencies are declared in `pom.xml` |
| Manage versions manually | Maven manages dependency versions |
| Manual build process | Automated build lifecycle |
| Difficult to manage many dependencies | Easier dependency management |
| No standard structure required | Uses standard project structure |

---

## Important Maven Terms

| Term | Meaning |
|---|---|
| Maven | Build automation and project management tool |
| POM | Project Object Model |
| `pom.xml` | Main Maven project configuration file |
| Dependency | External library required by a project |
| Repository | Location where Maven artifacts are stored |
| Maven Central | Public repository for many Maven artifacts |
| Local Repository | Dependency cache stored on the developer's machine |
| Artifact | File produced or managed by Maven |
| Plugin | Extension that provides Maven functionality |
| Lifecycle | Predefined sequence of build phases |

---

## Key Points

- Maven is mainly used for Java project build automation and dependency management.
- Maven uses `pom.xml` to manage project configuration.
- Dependencies can be declared inside `pom.xml`.
- Maven can download dependencies automatically.
- Maven Central is a major public repository.
- Maven stores downloaded dependencies in the local `.m2` repository.
- Maven follows a standard project structure.
- Maven uses plugins to perform different tasks.
- Maven provides predefined build lifecycles.
- Maven can compile, test, package, and install projects.

---

## In Simple Words

Maven makes Java project management easier by handling:

    Dependencies
    + 
    Build
    +
    Testing
    +
    Packaging
    +
    Project Configuration

Instead of managing these tasks manually, we define the project configuration in `pom.xml` and let Maven handle the build process.
