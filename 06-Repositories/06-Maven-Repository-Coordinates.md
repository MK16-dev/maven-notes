# Maven Repository Coordinates

Maven coordinates are a standard way of uniquely identifying an artifact.

The three most important coordinates are:

    groupId
    artifactId
    version

Together, they identify a specific Maven artifact.

---

# 1. `groupId`

`groupId` identifies the organization, company, or project group that owns the artifact.

Example:

    <groupId>com.example</groupId>

For commonly used libraries, the group ID usually represents the organization that publishes the library.

Examples:

    org.apache.commons
    org.springframework
    org.junit

---

# 2. `artifactId`

`artifactId` identifies the particular project or library.

Example:

    <artifactId>maven-demo</artifactId>

For our project:

    groupId    → com.example
    artifactId → maven-demo

---

# 3. `version`

`version` identifies the specific version of the artifact.

Our project uses:

    <version>1.0-SNAPSHOT</version>

Examples:

    1.0
    1.1
    2.0
    1.0-SNAPSHOT

---

# Complete Coordinates

Our project's coordinates are:

    com.example:maven-demo:1.0-SNAPSHOT

This can be read as:

    groupId:artifactId:version

    com.example
         :
    maven-demo
         :
    1.0-SNAPSHOT

---

# Coordinates and Repository Path

Maven uses these coordinates to determine where an artifact is stored in a repository.

For our project:

    groupId:
    com.example

    artifactId:
    maven-demo

    version:
    1.0-SNAPSHOT

The local repository path becomes:

    ~/.m2/repository/com/example/maven-demo/1.0-SNAPSHOT/

Notice that the dots in the `groupId` become directory separators:

    com.example
         ↓
    com/example

---

# Artifact File

Inside the version directory, Maven stores the artifact.

For our project:

    maven-demo-1.0-SNAPSHOT.jar

It also stores the project's POM:

    maven-demo-1.0-SNAPSHOT.pom

So the structure is approximately:

    ~/.m2/repository/
    └── com/
        └── example/
            └── maven-demo/
                └── 1.0-SNAPSHOT/
                    ├── maven-demo-1.0-SNAPSHOT.jar
                    ├── maven-demo-1.0-SNAPSHOT.pom
                    └── maven-metadata-local.xml

---

# Coordinates in Dependencies

The same coordinate system is used when declaring dependencies.

Example:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>3.18.0</version>
    </dependency>

The dependency coordinates are:

    org.apache.commons:commons-lang3:3.18.0

Maven uses these coordinates to locate the required artifact in its repositories.

---

# Why Coordinates Are Important

Coordinates allow Maven to uniquely identify artifacts.

Without a consistent identification system, Maven would not know exactly which library or version a project requires.

For example:

    org.apache.commons:commons-lang3:3.18.0

is different from:

    org.apache.commons:commons-lang3:3.17.0

because the versions are different.

---

# Key Points

- Maven coordinates uniquely identify an artifact.
- The three primary coordinates are `groupId`, `artifactId`, and `version`.
- Format:

      groupId:artifactId:version

- Our project coordinates are:

      com.example:maven-demo:1.0-SNAPSHOT

- Coordinates determine the artifact's repository path.
- `groupId` dots are converted into directory separators.
- Dependency declarations also use these coordinates.

---

# Interview Questions

### What are Maven coordinates?

They are identifiers used to uniquely identify a Maven artifact, primarily using `groupId`, `artifactId`, and `version`.

### What is the format of Maven coordinates?

    groupId:artifactId:version

### What are the coordinates of our Maven project?

    com.example:maven-demo:1.0-SNAPSHOT

### How does Maven convert `groupId` into a repository path?

Dots in the `groupId` are converted into directory separators.

For example:

    com.example

becomes:

    com/example

### Why is the version part of Maven coordinates?

Because multiple versions of the same artifact can exist, and Maven needs to identify exactly which version is required.

### Are Maven coordinates used only for our own project?

No. The same coordinate system is used to identify dependencies, plugins, and other Maven artifacts.
