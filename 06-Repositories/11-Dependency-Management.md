# Maven Dependency Management

Maven provides `<dependencyManagement>` to centrally control dependency versions and other dependency information.

It is commonly used in multi-module Maven projects.

---

# Why Use Dependency Management?

Suppose several modules use the same library.

Without dependency management, each module may have to specify the version separately:

    Module A → Library X → 1.0

    Module B → Library X → 1.0

    Module C → Library X → 1.0

This can become difficult to maintain.

With `<dependencyManagement>`, the version can be defined once and reused.

---

# Example

In a parent POM:

    <dependencyManagement>
        <dependencies>

            <dependency>
                <groupId>org.apache.commons</groupId>
                <artifactId>commons-lang3</artifactId>
                <version>3.18.0</version>
            </dependency>

        </dependencies>
    </dependencyManagement>

A child module can then declare:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
    </dependency>

The child module does not need to specify the version because it is inherited from `dependencyManagement`.

---

# Important Difference

`dependencyManagement` **does not automatically add a dependency to the project**.

It only manages information about the dependency.

For example:

    <dependencyManagement>
        ...
    </dependencyManagement>

defines the version.

The actual dependency still needs to be declared:

    <dependencies>
        ...
    </dependencies>

Therefore:

    dependencyManagement
        ↓
    Controls dependency information

    dependencies
        ↓
    Adds dependency to the project

---

# Multi-Module Maven Projects

Dependency management is especially useful when a project contains multiple modules.

Example:

    Parent Project
       ├── Module A
       ├── Module B
       └── Module C

The parent POM can define common dependency versions:

    Parent POM
        ↓
    dependencyManagement
        ↓
    ┌─────────┬─────────┬─────────┐
    ↓         ↓         ↓
    A         B         C
    ↓         ↓         ↓
  Uses      Uses      Uses
  same      same      same
  version   version   version

This keeps dependency versions consistent across modules.

---

# `dependencies` vs `dependencyManagement`

| `dependencies` | `dependencyManagement` |
|---|---|
| Adds dependencies to the project | Manages dependency information |
| Dependency is available to the project | Does not itself add the dependency |
| Used when the project actually needs the dependency | Commonly used to centralize versions |
| Can be defined in parent or child POM | Commonly defined in parent POM |

---

# Version Consistency

One major advantage of dependency management is centralized version control.

Instead of:

    Module A → Library X → 1.0

    Module B → Library X → 1.1

    Module C → Library X → 1.0

the parent can define:

    Library X → 1.1

and modules can use the managed version.

This reduces version inconsistencies across the project.

---

# BOM and Dependency Management

A BOM (Bill of Materials) is another important concept related to dependency management.

A BOM provides a set of compatible dependency versions that can be imported into a Maven project.

Example:

    <dependencyManagement>
        <dependencies>

            <dependency>
                <groupId>some.group</groupId>
                <artifactId>some-bom</artifactId>
                <version>1.0</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>

        </dependencies>
    </dependencyManagement>

The imported BOM can manage versions of multiple related dependencies.

This approach is widely used by frameworks and large projects.

---

# Important Interview Point

Remember this distinction:

    <dependencies>
        → Declares dependencies required by the project.

    <dependencyManagement>
        → Centrally manages dependency information, especially versions.

A dependency inside `dependencyManagement` is not automatically added to the project's classpath.

---

# Key Points

- `dependencyManagement` centrally manages dependency information.
- It is especially useful in multi-module projects.
- It can keep dependency versions consistent.
- It does not automatically add dependencies to the project.
- Child modules can inherit managed dependency versions.
- `dependencies` actually declares dependencies used by the project.
- BOMs can be imported through `dependencyManagement`.

---

# Interview Questions

### What is `dependencyManagement` in Maven?

It is used to centrally manage dependency information, especially dependency versions.

### Does `dependencyManagement` add a dependency to the project?

No. The dependency must still be declared under `<dependencies>`.

### Why is `dependencyManagement` useful?

It allows dependency versions to be managed centrally and consistently across multiple modules.

### What is the difference between `dependencies` and `dependencyManagement`?

`dependencies` declares dependencies that the project uses, while `dependencyManagement` manages dependency information that can be inherited or reused.

### Where is `dependencyManagement` commonly used?

It is commonly used in parent POMs of multi-module Maven projects.

### What is a BOM?

A Bill of Materials is a POM that provides a managed set of compatible dependency versions, which can be imported into `dependencyManagement`.
