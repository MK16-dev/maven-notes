# Maven Dependency Scopes

Dependency scope determines where a dependency is available during the Maven build and whether it is included in the final artifact.

Maven provides several dependency scopes.

The commonly used scopes are:

    compile
    provided
    runtime
    test
    system

`compile`, `provided`, `runtime`, and `test` are the most important for interviews and everyday Maven usage.

---

# 1. Compile Scope

`compile` is the default dependency scope.

If no scope is specified, Maven uses:

    compile

Example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

This is equivalent to:

    <scope>compile</scope>

A compile-scoped dependency is available during:

- Compilation
- Testing
- Runtime

It is also included as a dependency of the packaged application when appropriate.

---

# 2. Provided Scope

`provided` means the dependency is required to compile the application, but the runtime environment is expected to provide it.

Example:

    <dependency>
        <groupId>jakarta.servlet</groupId>
        <artifactId>jakarta.servlet-api</artifactId>
        <version>...</version>
        <scope>provided</scope>
    </dependency>

This is commonly used for APIs provided by an application server.

For example, a web application may need the Servlet API to compile, while the application server provides the API when the application runs.

---

# 3. Runtime Scope

`runtime` means the dependency is not required to compile the main source code, but it is required when the application runs.

Example:

    <dependency>
        <groupId>some.group</groupId>
        <artifactId>some-runtime-library</artifactId>
        <version>1.0</version>
        <scope>runtime</scope>
    </dependency>

A common example is a JDBC driver.

The application may compile against JDBC APIs while the actual database driver is needed at runtime.

---

# 4. Test Scope

`test` means the dependency is required only for compiling and running tests.

Example from our project:

    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>3.8.1</version>
        <scope>test</scope>
    </dependency>

This dependency is available during the test phase but is not required by the main application at runtime.

This is why testing libraries are commonly declared with:

    <scope>test</scope>

---

# 5. System Scope

`system` is similar to `provided`, but the dependency must be explicitly provided using a local file path.

Example:

    <scope>system</scope>

    <systemPath>...</systemPath>

This scope is generally discouraged because it makes the build dependent on a specific local file path.

It is rarely appropriate in modern Maven projects.

---

# Dependency Scope Comparison

| Scope | Compile | Test | Runtime | Typical Use |
|---|---|---|---|---|
| `compile` | Yes | Yes | Yes | Normal application dependency |
| `provided` | Yes | Yes | No | Dependency provided by runtime environment |
| `runtime` | No | Yes | Yes | Runtime-only libraries |
| `test` | No | Yes | No | Testing libraries |
| `system` | Yes | Yes | Yes | Local explicitly specified dependency |

---

# Default Scope

If `<scope>` is not specified, Maven uses:

    compile

For example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

is a compile-scoped dependency.

---

# Our Maven Project

Our `pom.xml` contains two dependencies.

### JUnit

    <scope>test</scope>

Therefore, JUnit is available for testing but is not required by the main application.

### Commons Lang

No scope is specified:

    org.apache.commons:commons-lang3:3.18.0

Therefore, Maven uses the default:

    compile

---

# Why Dependency Scope Matters

Dependency scope helps control the classpath and prevents unnecessary libraries from being included in parts of the application where they are not needed.

For example:

    JUnit
       ↓
    Test scope
       ↓
    Used for tests

while:

    Commons Lang
       ↓
    Compile scope
       ↓
    Available to application code

---

# Important Interview Point

A very common interview question is:

**What is the default Maven dependency scope?**

Answer:

    compile

Another common question:

**Which scope is normally used for JUnit?**

Answer:

    test

because JUnit is required for testing but not for running the production application.

---

# Key Points

- Dependency scope controls when a dependency is available.
- `compile` is the default scope.
- `provided` is used when the runtime environment provides the dependency.
- `runtime` is used for dependencies needed during runtime but not compilation.
- `test` is used only for testing.
- `system` uses a manually specified local path and is generally discouraged.
- Our JUnit dependency uses `test`.
- Our Commons Lang dependency uses the default `compile` scope.

---

# Interview Questions

### What is dependency scope in Maven?

It determines when and where a dependency is available during the Maven build and runtime.

### What is the default dependency scope?

`compile`.

### Which scope is commonly used for JUnit?

`test`.

### What is the purpose of `provided` scope?

It indicates that the dependency is needed for compilation but is expected to be supplied by the runtime environment.

### What is the purpose of `runtime` scope?

It is used when a dependency is needed at runtime but is not required to compile the main source code.

### What is the difference between `provided` and `runtime`?

`provided` dependencies are available during compilation but are expected to be supplied by the runtime environment. `runtime` dependencies are needed at runtime but are not required to compile the main application code.

### Why is `system` scope generally discouraged?

Because it requires an explicit local file path, making the build less portable between different machines.
