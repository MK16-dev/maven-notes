# Maven Dependency Exclusions

Maven normally includes transitive dependencies automatically.

Sometimes a project should not receive a particular transitive dependency. Maven provides `<exclusions>` to prevent a specific dependency from being included.

---

## Why Exclude a Dependency?

A transitive dependency may need to be excluded when:

- A different version is required.
- The dependency is unnecessary.
- Another library provides the same functionality.
- A dependency causes a conflict.
- A security or compatibility issue requires it to be removed.

---

# Example

Suppose:

    Project
       ↓
    Library A
       ↓
    Library B

Library B is a transitive dependency of the project.

If we do not want Library B, we can exclude it from Library A:

    <dependency>
        <groupId>com.example</groupId>
        <artifactId>library-a</artifactId>
        <version>1.0</version>

        <exclusions>

            <exclusion>
                <groupId>com.example</groupId>
                <artifactId>library-b</artifactId>
            </exclusion>

        </exclusions>

    </dependency>

Now Maven will not include Library B through Library A.

---

# How Exclusion Works

The exclusion is declared **inside the dependency that brings in the unwanted transitive dependency**.

Structure:

    <dependency>
        ...
        <exclusions>
            <exclusion>
                ...
            </exclusion>
        </exclusions>
    </dependency>

The `<exclusion>` identifies the dependency using its:

    groupId
    artifactId

---

# Multiple Exclusions

More than one dependency can be excluded from the same dependency.

Example:

    <exclusions>

        <exclusion>
            <groupId>com.example</groupId>
            <artifactId>library-b</artifactId>
        </exclusion>

        <exclusion>
            <groupId>com.example</groupId>
            <artifactId>library-c</artifactId>
        </exclusion>

    </exclusions>

This excludes both dependencies from being brought in transitively through that dependency.

---

# Finding What to Exclude

Before excluding a dependency, it is useful to understand where it comes from.

Use:

    mvn dependency:tree

Example:

    Project
    └── Library A
        └── Library B

If Library B is causing a problem, the dependency tree helps identify that Library A is bringing it into the project.

You can then configure an exclusion on Library A.

---

# Exclusion vs Optional Dependency

These concepts are related but different.

### Optional Dependency

A library marks one of its own dependencies as optional.

    <optional>true</optional>

This prevents the dependency from being automatically propagated to consumers.

### Exclusion

A project explicitly prevents a transitive dependency from being included.

    <exclusions>
        <exclusion>
            ...
        </exclusion>
    </exclusions>

Therefore:

    Optional
    → Controlled by the project providing the dependency

    Exclusion
    → Controlled by the project consuming the dependency

---

# Important Interview Point

An exclusion is not a global rule for Maven.

It applies to the dependency where the exclusion is declared.

For example:

    Project
       ↓
    Library A
       ↓
    Library B

If B is excluded from A, Maven will not obtain B through A.

However, if another dependency brings B into the project through a different path, that dependency may still bring B in.

This is why `mvn dependency:tree` is useful when troubleshooting dependency problems.

---

# Key Points

- Maven automatically resolves transitive dependencies.
- `<exclusions>` prevents a specific transitive dependency from being included through a dependency.
- Exclusions use `groupId` and `artifactId` to identify the dependency.
- `mvn dependency:tree` helps determine where a dependency comes from.
- An exclusion applies to the dependency where it is declared.
- Exclusion and optional dependency are different concepts.

---

# Interview Questions

### What is dependency exclusion in Maven?

It is a mechanism used to prevent a specific transitive dependency from being included through another dependency.

### Why would you exclude a dependency?

To avoid conflicts, unnecessary dependencies, incompatible versions, or other dependency-related problems.

### How do you exclude a transitive dependency?

Using `<exclusions>` inside the dependency that brings in the unwanted dependency.

### How do you find which dependency is bringing in an unwanted library?

Run:

    mvn dependency:tree

### What is the difference between optional dependency and exclusion?

An optional dependency is marked by the project providing it and is not automatically propagated to consumers. An exclusion is explicitly configured by the consuming project to prevent a transitive dependency from being included.

### Is an exclusion global?

No. It applies to the dependency where the exclusion is configured.
