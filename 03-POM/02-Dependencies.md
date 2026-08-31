# Maven Dependencies

A dependency is an external library that a Maven project requires to compile, test, or run.

Instead of manually downloading JAR files and adding them to the project, Maven allows dependencies to be declared in the `pom.xml` file.

Maven then resolves and downloads the required dependencies automatically.

---

## Declaring a Dependency

Dependencies are declared inside the `<dependencies>` section of `pom.xml`.

Example:

    <dependencies>

        <dependency>
            <groupId>org.apache.commons</groupId>
            <artifactId>commons-lang3</artifactId>
            <version>3.18.0</version>
        </dependency>

    </dependencies>

Maven reads this configuration and downloads the required library from a configured repository, normally Maven Central.

---

## Dependency Coordinates

A dependency is identified using Maven coordinates.

The main coordinates are:

- `groupId`
- `artifactId`
- `version`

Example:

    <groupId>org.apache.commons</groupId>
    <artifactId>commons-lang3</artifactId>
    <version>3.18.0</version>

These values uniquely identify the dependency version that Maven should use.

---

## 1. `groupId`

The `groupId` identifies the organization or group that provides the dependency.

Example:

    <groupId>org.apache.commons</groupId>

Apache Commons is the organization/group providing the library.

---

## 2. `artifactId`

The `artifactId` identifies the specific library.

Example:

    <artifactId>commons-lang3</artifactId>

This identifies Apache Commons Lang 3.

---

## 3. `version`

The `version` specifies the exact version of the dependency.

Example:

    <version>3.18.0</version>

Using an explicit version makes the project's dependency configuration predictable and reproducible.

---

# Example: JUnit Dependency

Our project contains JUnit as a test dependency:

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
    </dependency>

The important part is:

    <scope>test</scope>

This means the dependency is available for compiling and running tests, but it is not required as a normal application dependency at runtime.

---

# Example: Apache Commons Lang

Our project also uses Apache Commons Lang:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

Because no scope is specified, Maven uses the default `compile` scope.

This dependency is therefore available during:

- Compilation
- Testing
- Runtime

We used `StringUtils` from this library in our Java application.

---

# Dependency Scope

Dependency scope determines when and where a dependency is available.

The main Maven scopes are:

| Scope | Compile | Test | Runtime | Packaged |
|---|---|---|---|---|
| `compile` | Yes | Yes | Yes | Yes |
| `provided` | Yes | Yes | Yes | No |
| `runtime` | No | Yes | Yes | Yes |
| `test` | No | Yes | No | No |
| `system` | Yes | Yes | Yes | No |

---

## Compile Scope

`compile` is the default scope.

Example:

    <scope>compile</scope>

If the scope is omitted, Maven uses `compile`.

Compile dependencies are available during:

- Compilation
- Testing
- Runtime

Example:

    commons-lang3

---

## Test Scope

Test dependencies are used only for testing.

Example:

    <scope>test</scope>

JUnit is a common example.

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
    </dependency>

Test dependencies are not included as normal application dependencies.

---

## Provided Scope

`provided` dependencies are required to compile and test the application but are expected to be provided by the runtime environment.

A common example is a Servlet API dependency in a web application where the application server provides the API.

Example:

    <scope>provided</scope>

---

## Runtime Scope

`runtime` dependencies are not required to compile the application but are required when the application runs.

Example:

    <scope>runtime</scope>

A database JDBC driver can commonly be used with runtime scope when the application does not directly reference driver classes during compilation.

---

## System Scope

`system` dependencies refer to a specific JAR on the local system.

Example:

    <scope>system</scope>

This scope is generally discouraged because it makes the project dependent on a specific local file path.

Maven Central or another repository should normally be preferred.

---

# Transitive Dependencies

A dependency can itself depend on other libraries.

For example:

    Project
       ↓
    Dependency A
       ↓
    Dependency B

If Dependency A requires Dependency B, Maven can automatically bring Dependency B into the project.

This is called a **transitive dependency**.

Without Maven, developers would often have to manually identify and download these additional libraries.

---

# Direct vs Transitive Dependencies

### Direct Dependency

A dependency explicitly declared in your own `pom.xml`.

Example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

### Transitive Dependency

A dependency that Maven brings in because another dependency requires it.

Example:

    Project
       ↓
    Library A
       ↓
    Library B

Library B is a transitive dependency of the project.

---

# Dependency Tree

Maven provides a useful command for viewing dependencies and their relationships:

    mvn dependency:tree

This displays the project's dependency tree.

Example:

    [INFO] com.example:maven-demo:jar:1.0-SNAPSHOT
    [INFO] +- org.apache.commons:commons-lang3:jar:3.18.0:compile
    [INFO] \- junit:junit:jar:3.8.1:test

The dependency tree helps identify:

- Direct dependencies
- Transitive dependencies
- Dependency versions
- Dependency scopes
- Dependency conflicts

---

# Dependency Resolution

When Maven encounters a dependency, it attempts to resolve it using repositories.

The general process is:

    pom.xml
       ↓
    Dependency declaration
       ↓
    Maven checks local repository
       ↓
    If unavailable, Maven accesses a remote repository
       ↓
    Dependency is downloaded
       ↓
    Dependency is stored locally
       ↓
    Maven uses it during the build

---

# Local Maven Repository

Maven stores downloaded dependencies in the local repository.

On Windows:

    C:\Users\<username>\.m2\repository

For example:

    C:\Users\mital\.m2\repository

The local repository acts as a cache.

Once a dependency has been downloaded, Maven can normally reuse the locally stored copy instead of downloading it again.

---

# Maven Central

Maven Central is a major public repository containing Java libraries and Maven artifacts.

When Maven needs a dependency that is not already available locally, it can download it from a configured remote repository such as Maven Central.

For example, during our project build Maven downloaded:

    commons-lang3-3.18.0.jar

from the Maven repository.

---

# Dependency Conflict

A dependency conflict can occur when different dependencies require different versions of the same library.

Example:

    Project
       ├── Library A
       │      └── commons-library 1.0
       │
       └── Library B
              └── commons-library 2.0

Maven has dependency resolution rules for determining which version should be used.

The dependency tree can be used to investigate such situations:

    mvn dependency:tree

---

# Excluding a Transitive Dependency

Sometimes a transitive dependency is not required or causes a conflict.

Maven allows a transitive dependency to be excluded.

Example:

    <dependency>
        <groupId>com.example</groupId>
        <artifactId>library-a</artifactId>
        <version>1.0</version>

        <exclusions>
            <exclusion>
                <groupId>org.example</groupId>
                <artifactId>library-b</artifactId>
            </exclusion>
        </exclusions>

    </dependency>

The `<exclusions>` element prevents the specified transitive dependency from being included through that dependency.

---

# Adding a New Dependency

To add a dependency:

### Step 1

Find the required library and its Maven coordinates.

### Step 2

Add the dependency inside `<dependencies>` in `pom.xml`.

### Step 3

Save the POM.

### Step 4

Run a Maven command such as:

    mvn compile

Maven will resolve the dependency and download it if necessary.

---

# Example from Our Project

Our `pom.xml` contains:

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

Here:

- JUnit is used for testing.
- Apache Commons Lang is a compile dependency.
- Maven downloads the required JAR files automatically.
- The dependencies are stored in the local `.m2` repository.
- Maven makes the dependencies available during the appropriate build phases.

---

# Important Commands

### Display the dependency tree

    mvn dependency:tree

### Compile the project

    mvn compile

### Run tests

    mvn test

### Package the project

    mvn package

### Clean the project

    mvn clean

---

# Why Maven Dependencies Are Useful

Without Maven, a developer may need to:

- Search for library JAR files manually.
- Download the correct versions.
- Add JARs to the project manually.
- Find additional libraries required by those JARs.
- Manage different library versions manually.

Maven automates much of this process through dependency management.

---

# Key Points

- Dependencies are external libraries required by a Maven project.
- Dependencies are declared inside `<dependencies>` in `pom.xml`.
- Maven coordinates identify a dependency.
- The main coordinates are `groupId`, `artifactId`, and `version`.
- Dependency scope controls when a dependency is available.
- `compile` is the default dependency scope.
- `test` dependencies are available only for testing.
- Maven supports transitive dependencies.
- `mvn dependency:tree` displays the dependency hierarchy.
- Maven stores downloaded dependencies in the local `.m2` repository.
- Maven can download dependencies from remote repositories such as Maven Central.
- Dependency exclusions can be used to prevent unwanted transitive dependencies.

---

# Quick Reference

| Concept | Purpose |
|---|---|
| Dependency | External library required by a project |
| `groupId` | Identifies the dependency group/organization |
| `artifactId` | Identifies the specific library |
| `version` | Specifies the dependency version |
| `scope` | Defines when the dependency is available |
| Transitive dependency | Dependency brought in by another dependency |
| Local repository | Stores downloaded Maven artifacts locally |
| Maven Central | Public repository for Maven artifacts |
| `mvn dependency:tree` | Displays the dependency hierarchy |
| `<exclusions>` | Excludes a transitive dependency |

---

# Summary

Maven dependency management allows a project to declare the libraries it needs in `pom.xml`.

Maven then handles dependency resolution, downloading, version management, and making the libraries available during the appropriate stages of the build.

This makes Java projects easier to build, maintain, and reproduce across different environments.
