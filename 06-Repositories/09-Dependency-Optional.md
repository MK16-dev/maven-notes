# Maven Optional Dependencies

An optional dependency is a dependency that is required by one Maven project but is not automatically passed on to projects that depend on it.

It is configured using:

    <optional>true</optional>

---

## Normal Dependency Behavior

Consider three projects:

    Project A
       ↓
    Library B
       ↓
    Library C

If Library B declares Library C as a normal dependency, Project A can normally receive Library C transitively.

The dependency is passed through the dependency chain.

---

# Optional Dependency

Now suppose Library B declares Library C as:

    <dependency>
        <groupId>com.example</groupId>
        <artifactId>library-c</artifactId>
        <version>1.0</version>
        <optional>true</optional>
    </dependency>

The relationship becomes:

    Project A
       ↓
    Library B
       ↓
    Library C
    (optional)

Library C is available to Library B, but it is not automatically included as a transitive dependency of Project A.

If Project A needs Library C, Project A must declare it explicitly.

---

# Why Use Optional Dependencies?

Optional dependencies are useful when a library supports additional features that not every user needs.

For example, a library might support multiple technologies:

    Main Library
       ├── Feature A
       ├── Feature B
       └── Feature C

If Feature C requires an additional library, that dependency can be marked optional so users who do not use Feature C do not automatically receive that extra dependency.

This helps avoid unnecessary transitive dependencies.

---

# Syntax

Example:

    <dependency>
        <groupId>com.example</groupId>
        <artifactId>optional-library</artifactId>
        <version>1.0</version>
        <optional>true</optional>
    </dependency>

The important part is:

    <optional>true</optional>

---

# Optional vs Normal Dependency

### Normal Dependency

A normal dependency can be propagated transitively to projects that depend on your project.

### Optional Dependency

An optional dependency is available to your project but is not automatically propagated to projects that depend on your project.

---

# Important Interview Example

Suppose:

    Application A
         ↓
    Library B
         ↓
    Library C

If Library C is a normal dependency of B:

    A → B → C

C can be available transitively to A.

If C is optional:

    A → B

C is not automatically provided to A.

If A needs C, A must declare C directly.

---

# Optional Dependency vs Dependency Scope

Do not confuse optional dependencies with dependency scopes.

### Scope

Controls when a dependency is available during the build and runtime.

Examples:

    compile
    test
    runtime
    provided

### Optional

Controls whether a dependency is propagated transitively to consumers of your project.

Therefore:

    Scope → When/where the dependency is available

    Optional → Whether it is propagated transitively

---

# Important Interview Point

`<optional>true</optional>` does **not** mean that the dependency is optional for your own project.

It means that the dependency is optional for projects that consume your project.

For your project, the dependency is still available according to its configured scope.

---

# Key Points

- Optional dependencies are configured using `<optional>true</optional>`.
- They are available to the project that declares them.
- They are not automatically propagated transitively to consuming projects.
- A consuming project must declare an optional dependency explicitly if it needs it.
- Optional dependencies can prevent unnecessary transitive dependencies.
- Optional dependencies and dependency scopes solve different problems.

---

# Interview Questions

### What is an optional dependency in Maven?

It is a dependency available to the project that declares it but not automatically propagated to projects that depend on that project.

### How do you declare an optional dependency?

Using:

    <optional>true</optional>

### Does optional mean the dependency is not available to the current project?

No. The current project can still use it. Optional controls its transitive propagation to consumers.

### Why are optional dependencies useful?

They allow libraries to provide additional features without forcing every consumer to receive all related dependencies.

### What is the difference between optional dependency and dependency scope?

Scope controls when and where a dependency is available, while optional controls whether the dependency is propagated transitively to consumers.
