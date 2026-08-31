# Maven Dependency Resolution

Maven dependency resolution is the process Maven uses to find, download, and make the required dependencies available to a project.

When a dependency is declared in `pom.xml`, Maven determines where to get it from and which version should be used.

---

## Dependency Resolution Flow

When Maven encounters a dependency, the general process is:

    pom.xml
       ↓
    Read dependency coordinates
       ↓
    Check Local Repository
       ↓
    Dependency available?
       ↓
    Yes → Use local artifact
       ↓
    No → Check configured remote repositories
       ↓
    Download dependency
       ↓
    Store it in Local Repository
       ↓
    Add it to the project classpath

---

## Example

Our project contains:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

Maven identifies this dependency using:

    org.apache.commons:commons-lang3:3.18.0

Maven then looks for the required artifact in its repositories.

Once downloaded, it is stored locally under a path similar to:

    ~/.m2/repository/org/apache/commons/commons-lang3/3.18.0/

---

# Transitive Dependencies

One of Maven's important features is **transitive dependency management**.

A dependency can itself depend on other libraries.

For example:

    Project
       ↓
    Dependency A
       ↓
    Dependency B

If your project requires Dependency A, Maven can also resolve Dependency B when it is required by A.

You therefore do not always need to explicitly declare every library used indirectly by your dependencies.

---

## Example of a Transitive Dependency

Suppose:

    Project
       ↓
    Library A
       ↓
    Library B

If Library A declares Library B as a dependency, Maven can automatically bring Library B into the project.

This is called a **transitive dependency**.

---

# Direct vs Transitive Dependency

### Direct Dependency

A dependency that you explicitly declare in your `pom.xml`.

Example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

### Transitive Dependency

A dependency that is brought into your project because one of your direct dependencies requires it.

Example:

    Your Project
         ↓
    Direct Dependency
         ↓
    Transitive Dependency

---

# Viewing Dependency Resolution

Maven provides the `dependency:tree` goal to display the project's dependency hierarchy.

Command:

    mvn dependency:tree

It displays dependencies in a tree-like structure.

Example:

    com.example:maven-demo
    └── org.apache.commons:commons-lang3:3.18.0

For a larger project, the output can show dependencies several levels deep.

---

# Why `dependency:tree` Is Useful

It can help identify:

- Which dependencies are present.
- Which dependencies are transitive.
- Different versions of the same dependency.
- Where a dependency came from.
- Potential dependency conflicts.

This makes it an important troubleshooting command.

---

# Dependency Conflict

A dependency conflict can occur when different dependencies require different versions of the same library.

For example:

    Library A
       ↓
    commons-library:1.0

    Library B
       ↓
    commons-library:2.0

Your project now has two different requested versions.

Maven uses dependency mediation rules to determine which version should be used.

---

# Nearest Definition

One important Maven dependency mediation rule is the **nearest definition**.

Conceptually:

    Project
       ↓
    A
       ↓
    B
       ↓
    C:1.0

and:

    Project
       ↓
    D
       ↓
    C:2.0

If Maven determines that one version is nearer to the project in the dependency tree, that version can be selected.

For complex dependency conflicts, the dependency tree should be inspected rather than guessing.

---

# Excluding a Transitive Dependency

Sometimes a transitive dependency is not wanted.

Maven allows a transitive dependency to be excluded.

Example:

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

This tells Maven not to include `library-b` through `library-a`.

---

# Important Interview Point

Maven does not simply download every dependency listed in `pom.xml` independently.

It also builds a dependency graph and resolves transitive dependencies.

This is why a single dependency declaration can result in multiple libraries being available to the project.

---

# Key Points

- Dependency resolution is the process Maven uses to obtain required artifacts.
- Maven checks the local repository before downloading an artifact.
- Missing artifacts can be downloaded from configured remote repositories.
- Dependencies can have their own dependencies.
- Dependencies brought in indirectly are called transitive dependencies.
- `mvn dependency:tree` displays the dependency hierarchy.
- Dependency conflicts can occur when different libraries require different versions.
- Maven uses dependency mediation rules when resolving version conflicts.
- Transitive dependencies can be excluded using `<exclusions>`.

---

# Interview Questions

### What is dependency resolution in Maven?

It is the process Maven uses to locate, download, and make project dependencies available.

### What is a transitive dependency?

A dependency that is automatically included because it is required by another dependency.

### What is the difference between direct and transitive dependencies?

A direct dependency is explicitly declared in your `pom.xml`; a transitive dependency is brought in indirectly through another dependency.

### How do you see the dependency hierarchy?

Run:

    mvn dependency:tree

### Why is `mvn dependency:tree` useful?

It helps identify dependencies, transitive dependencies, dependency versions, and potential conflicts.

### What happens if two dependencies require different versions of the same library?

Maven applies dependency mediation rules to determine which version is selected. The dependency tree can be used to understand the result.

### Can a transitive dependency be excluded?

Yes. The `<exclusions>` element can be used to prevent a transitive dependency from being included.
