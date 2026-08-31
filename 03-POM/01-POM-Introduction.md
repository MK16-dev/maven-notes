# POM (Project Object Model)

POM stands for **Project Object Model**.

The POM is the core configuration of a Maven project. It is written in an XML file named:

    pom.xml

Maven reads the `pom.xml` file to understand the project, its dependencies, build configuration, plugins, and other settings.

---

## Why is `pom.xml` Important?

The `pom.xml` file tells Maven how the project should be managed and built.

It can define:

- Project information
- Maven coordinates
- Dependencies
- Plugins
- Build configuration
- Packaging type
- Project properties
- Repository configuration
- Build profiles

Instead of configuring these things manually, Maven uses the information provided in `pom.xml`.

---

## Basic POM Structure

A simple Maven `pom.xml` looks like this:

    <project>
        <modelVersion>4.0.0</modelVersion>

        <groupId>com.example</groupId>
        <artifactId>maven-demo</artifactId>
        <version>1.0-SNAPSHOT</version>

        <packaging>jar</packaging>

        <dependencies>
            ...
        </dependencies>

        <build>
            ...
        </build>
    </project>

The `<project>` element is the root element of the POM.

---

## 1. `modelVersion`

Example:

    <modelVersion>4.0.0</modelVersion>

This specifies the version of the POM model being used.

The standard Maven POM model version is:

    4.0.0

It does not represent the version of Maven itself.

---

## 2. `groupId`

Example:

    <groupId>com.example</groupId>

`groupId` identifies the organization, company, group, or project namespace.

It is commonly written using a reverse-domain naming convention.

Examples:

    com.example
    com.company
    org.apache

For our project:

    <groupId>com.example</groupId>

---

## 3. `artifactId`

Example:

    <artifactId>maven-demo</artifactId>

`artifactId` identifies the project or artifact within the group.

For our project:

    maven-demo

The artifact ID is also used when Maven creates the packaged artifact.

For example:

    maven-demo-1.0-SNAPSHOT.jar

---

## 4. `version`

Example:

    <version>1.0-SNAPSHOT</version>

The `version` identifies the version of the project.

Examples:

    1.0
    1.0.1
    2.0
    1.0-SNAPSHOT

`SNAPSHOT` generally indicates a development version that may still change.

Our project uses:

    1.0-SNAPSHOT

---

## Maven Coordinates

The combination of:

    groupId
    artifactId
    version

is commonly referred to as the Maven coordinates of an artifact.

Example:

    groupId    = com.example
    artifactId = maven-demo
    version    = 1.0-SNAPSHOT

These coordinates allow Maven to identify the artifact.

---

## 5. `packaging`

Example:

    <packaging>jar</packaging>

The `packaging` element specifies the type of artifact Maven should produce.

Common packaging types include:

| Packaging | Description |
|---|---|
| `jar` | Java Archive |
| `war` | Web Application Archive |
| `pom` | POM project |
| `ear` | Enterprise Application Archive |

If `<packaging>` is not specified, Maven uses:

    jar

For our project:

    <packaging>jar</packaging>

Maven therefore creates:

    maven-demo-1.0-SNAPSHOT.jar

---

## 6. `name`

Example:

    <name>maven-demo</name>

The `<name>` element provides a human-readable name for the project.

It is mainly project metadata and does not determine the artifact name.

---

## 7. `url`

Example:

    <url>http://maven.apache.org</url>

The `<url>` element can contain the project's website.

It is optional.

---

# Dependencies

A dependency is an external library required by the project.

Dependencies are declared inside:

    <dependencies>

        ...

    </dependencies>

For example, our project uses Apache Commons Lang.

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

Maven uses the dependency coordinates to locate and download the required library.

---

## Dependency Elements

A dependency normally contains:

    groupId
    artifactId
    version
    scope

Example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

### `groupId`

Identifies the organization or group that provides the dependency.

### `artifactId`

Identifies the dependency.

### `version`

Specifies which version of the dependency should be used.

### `scope`

Defines where the dependency is required.

---

## Dependency Scope

Common Maven dependency scopes include:

| Scope | Purpose |
|---|---|
| `compile` | Available during compilation, testing, and runtime |
| `provided` | Required for compilation but normally supplied by the runtime environment |
| `runtime` | Required at runtime but not for compilation |
| `test` | Available only during testing |
| `system` | Uses a dependency from a specified local system path |

Example:

    <scope>test</scope>

Our JUnit dependency uses the `test` scope because it is required only for running tests.

---

# Build Section

The `<build>` section contains build-related configuration.

Example:

    <build>
        <plugins>
            ...
        </plugins>
    </build>

It can contain configuration for:

- Plugins
- Source directories
- Output directories
- Resource directories
- Build-related settings

---

# Plugins

Maven plugins provide functionality for different tasks.

For example, our project uses the Exec Maven Plugin:

    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.5.0</version>
    </plugin>

This allowed us to run the Java application using:

    mvn exec:java -Dexec.mainClass=com.example.App

Plugins are covered in more detail in the `04-Plugins` section.

---

# Properties

The `<properties>` section can be used to define reusable configuration values.

Example:

    <properties>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

Properties help avoid repeating the same values throughout the POM.

They can also be referenced using:

    ${property-name}

For example:

    ${maven.compiler.source}

---

# Repositories

Maven uses repositories to obtain project artifacts and dependencies.

A repository can contain:

- Dependencies
- Plugins
- Maven artifacts
- Metadata

One of the main public repositories is Maven Central.

When Maven downloads a dependency, the dependency can also be stored in the local repository.

---

# Local Repository

Maven maintains a local repository on the developer's machine.

On Windows, it is normally:

    C:\Users\<username>\.m2\repository

For our system:

    C:\Users\mital\.m2\repository

After running:

    mvn install

our project was installed into:

    C:\Users\mital\.m2\repository\com\example\maven-demo\1.0-SNAPSHOT

The directory contained:

    maven-demo-1.0-SNAPSHOT.jar
    maven-demo-1.0-SNAPSHOT.pom
    maven-metadata-local.xml

This allows Maven to use the installed artifact locally.

---

# Complete `pom.xml` Example

The `pom.xml` we created for our Maven project contains:

    <project xmlns="http://maven.apache.org/POM/4.0.0"
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
             http://maven.apache.org/maven-v4_0_0.xsd">

        <modelVersion>4.0.0</modelVersion>

        <groupId>com.example</groupId>
        <artifactId>maven-demo</artifactId>
        <version>1.0-SNAPSHOT</version>
        <packaging>jar</packaging>

        <name>maven-demo</name>

        <dependencies>

            <dependency>
                <groupId>junit</groupId>
                <artifactId>junit</artifactId>
                <version>3.8.1</version>
                <scope>test</scope>
            </dependency>

            <dependency>
                <groupId>org.apache.commons</groupId>
                <artifactId>commons-lang3</artifactId>
                <version>3.18.0</version>
            </dependency>

        </dependencies>

        <build>
            <plugins>

                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>exec-maven-plugin</artifactId>
                    <version>3.5.0</version>
                </plugin>

            </plugins>
        </build>

    </project>

---

# Understanding Our POM

Our POM tells Maven that:

- The project belongs to the `com.example` group.
- The project is named `maven-demo`.
- The project version is `1.0-SNAPSHOT`.
- The project produces a JAR file.
- JUnit is required for testing.
- Apache Commons Lang is a project dependency.
- The Exec Maven Plugin is available for running the application.

Maven reads this configuration and uses it during the build process.

---

# Important POM Sections

| Element | Purpose |
|---|---|
| `<modelVersion>` | Defines the POM model version |
| `<groupId>` | Identifies the project group |
| `<artifactId>` | Identifies the project/artifact |
| `<version>` | Defines the project version |
| `<packaging>` | Defines the artifact type |
| `<name>` | Provides a project name |
| `<dependencies>` | Defines project dependencies |
| `<dependency>` | Defines an individual dependency |
| `<properties>` | Defines reusable configuration values |
| `<build>` | Contains build configuration |
| `<plugins>` | Defines Maven plugins |
| `<plugin>` | Defines an individual plugin |
| `<repositories>` | Defines additional artifact repositories |

---

# POM Hierarchy

Maven projects can inherit configuration from other POM files.

A project can have:

    Parent POM
         ↓
    Project POM
         ↓
    Module POM

This allows common configuration to be shared across multiple Maven projects.

Parent POMs are especially useful in larger projects and multi-module applications.

---

# Key Points

- POM stands for **Project Object Model**.
- Maven projects use `pom.xml` as their main configuration file.
- The POM defines project information and build configuration.
- `groupId`, `artifactId`, and `version` form the Maven coordinates.
- Dependencies are declared inside `<dependencies>`.
- Plugins are configured inside `<build>`.
- `<packaging>` determines the type of artifact produced.
- Properties provide reusable configuration values.
- Maven can inherit configuration from a parent POM.
- A well-configured POM allows Maven to manage the project consistently.

---

# In Simple Terms

The `pom.xml` is the **instruction and configuration file for a Maven project**.

It tells Maven:

    What is the project?
           ↓
    What version is it?
           ↓
    What dependencies does it need?
           ↓
    What plugins should be used?
           ↓
    How should the project be built?
           ↓
    What artifact should be produced?

Maven reads the POM and uses this information to manage the project throughout its build lifecycle.
