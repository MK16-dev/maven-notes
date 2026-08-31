# Maven Coordinates

Maven coordinates are identifiers used to uniquely identify a Maven project or artifact.

The main Maven coordinates are:

- `groupId`
- `artifactId`
- `version`

Together, they identify a specific artifact.

---

## Basic Structure

Example:

    <groupId>com.example</groupId>
    <artifactId>maven-demo</artifactId>
    <version>1.0-SNAPSHOT</version>

These coordinates identify our Maven project as:

    com.example:maven-demo:1.0-SNAPSHOT

---

# 1. `groupId`

The `groupId` identifies the organization, company, or group that owns or produces the project.

Example:

    <groupId>com.example</groupId>

Organizations commonly use reverse-domain naming.

Examples:

    com.google
    org.apache
    com.company
    com.example

The `groupId` helps prevent naming conflicts between projects.

---

# 2. `artifactId`

The `artifactId` identifies the specific project or artifact.

Example:

    <artifactId>maven-demo</artifactId>

For our project:

    maven-demo

The artifact ID is also used when Maven generates the artifact.

For example:

    maven-demo-1.0-SNAPSHOT.jar

---

# 3. `version`

The `version` identifies the version of the project or artifact.

Example:

    <version>1.0-SNAPSHOT</version>

Common examples:

    1.0
    1.0.1
    2.0
    1.0-SNAPSHOT

`SNAPSHOT` generally indicates that the version is still under development.

---

# Maven Coordinate Format

Coordinates are commonly represented as:

    groupId:artifactId:version

Example:

    com.example:maven-demo:1.0-SNAPSHOT

For a dependency:

    org.apache.commons:commons-lang3:3.18.0

This makes it easy to identify exactly which artifact is being referenced.

---

# Coordinates and Packaging

A Maven artifact also has a packaging/type.

For example:

    groupId    = com.example
    artifactId = maven-demo
    version    = 1.0-SNAPSHOT
    packaging  = jar

The resulting artifact is:

    maven-demo-1.0-SNAPSHOT.jar

The packaging is usually associated with the artifact type, while the three main coordinates identify the artifact itself.

---

# Coordinates in Dependencies

When declaring a dependency, Maven uses coordinates to identify the required library.

Example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

This identifies:

    org.apache.commons:commons-lang3:3.18.0

Maven uses these coordinates to locate and resolve the dependency.

---

# Coordinates and Local Repository

Maven uses coordinates to determine where artifacts are stored in the local repository.

For our project:

    groupId    = com.example
    artifactId = maven-demo
    version    = 1.0-SNAPSHOT

Maven stores the project under:

    ~/.m2/repository/com/example/maven-demo/1.0-SNAPSHOT/

On Windows, this is approximately:

    C:\Users\mital\.m2\repository\com\example\maven-demo\1.0-SNAPSHOT\

The directory contains files such as:

    maven-demo-1.0-SNAPSHOT.jar
    maven-demo-1.0-SNAPSHOT.pom

---

# SNAPSHOT Version

A version containing:

    SNAPSHOT

usually represents a development version.

Example:

    1.0-SNAPSHOT

It indicates that the artifact may change while development continues.

A released version might instead be:

    1.0

or:

    1.0.1

---

# Release Version

A release version represents a specific released version of an artifact.

Example:

    1.0

Once released, that version should normally remain unchanged.

This helps make builds reproducible.

---

# Why Maven Coordinates Are Important

Coordinates allow Maven to:

- Identify projects and artifacts.
- Resolve dependencies.
- Store artifacts in the correct repository location.
- Distinguish different versions of the same artifact.
- Prevent naming conflicts.
- Reference artifacts consistently.

---

# Example

Suppose we have:

    <groupId>com.company</groupId>
    <artifactId>employee-app</artifactId>
    <version>2.0</version>

The coordinates are:

    com.company:employee-app:2.0

If the project produces a JAR, the artifact can be:

    employee-app-2.0.jar

---

# Quick Reference

| Coordinate | Purpose | Example |
|---|---|---|
| `groupId` | Identifies the organization/group | `com.example` |
| `artifactId` | Identifies the project/artifact | `maven-demo` |
| `version` | Identifies the artifact version | `1.0-SNAPSHOT` |

Complete coordinates:

    com.example:maven-demo:1.0-SNAPSHOT

---

# Key Points

- Maven coordinates identify an artifact.
- The three main coordinates are `groupId`, `artifactId`, and `version`.
- Coordinates are commonly written as `groupId:artifactId:version`.
- `groupId` identifies the organization or group.
- `artifactId` identifies the project or artifact.
- `version` identifies the artifact version.
- `SNAPSHOT` generally represents a development version.
- Coordinates are used for dependency resolution and repository storage.
