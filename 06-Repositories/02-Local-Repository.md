# Maven Local Repository

The Maven Local Repository is a directory on the developer's machine where Maven stores downloaded dependencies, plugins, and locally installed project artifacts.

---

# Location

By default, the local repository is located at:

    ~/.m2/repository

On Windows:

    C:\Users\<username>\.m2\repository

For our system, it is:

    C:\Users\mital\.m2\repository

---

# What Is Stored in the Local Repository?

The local repository can contain:

- Downloaded dependencies
- Maven plugins
- POM files
- JAR files
- Artifacts installed using `mvn install`

For example, our project was installed at:

    ~/.m2/repository/com/example/maven-demo/1.0-SNAPSHOT/

It contained:

    maven-demo-1.0-SNAPSHOT.jar
    maven-demo-1.0-SNAPSHOT.pom
    maven-metadata-local.xml

---

# How Dependencies Reach the Local Repository

When Maven needs a dependency, it checks the local repository first.

If the dependency is not available, Maven downloads it from a configured remote repository and stores it locally.

The flow is:

    pom.xml
       ↓
    Maven checks ~/.m2/repository
       ↓
    Dependency available?
       ↓
    Yes → Use it
       ↓
    No → Download from remote repository
              ↓
        Store in local repository

This allows Maven to reuse downloaded dependencies in future builds.

---

# `mvn install` and Local Repository

The `install` phase is especially important because it installs your project's artifact into the local repository.

Command:

    mvn install

For our project:

    maven-demo-1.0-SNAPSHOT.jar

was installed into:

    ~/.m2/repository/com/example/maven-demo/1.0-SNAPSHOT/

After installation, another local Maven project can use this artifact as a dependency.

---

# Local Repository vs `target/`

These directories have different purposes.

### `target/`

Contains files generated during the current project build.

Examples:

    target/classes/
    target/test-classes/
    target/surefire-reports/
    target/maven-demo-1.0-SNAPSHOT.jar

### `.m2/repository/`

Stores Maven artifacts that are available for dependency resolution.

Examples:

    downloaded dependencies
    downloaded plugins
    installed project artifacts

Therefore:

    target/             → Project build output

    ~/.m2/repository/   → Maven's local artifact repository

---

# Clearing the Local Repository

The local repository should not normally be deleted just to fix ordinary Maven issues.

If an artifact is corrupted or a fresh download is required, the relevant artifact directory can be removed and Maven can download it again.

For example, if a particular dependency is corrupted:

    ~/.m2/repository/<groupId>/<artifactId>/<version>/

can be removed.

Maven will download it again when required.

---

# Important Interview Point

The local repository is different from the source code repository.

For example:

    GitHub
       ↓
    Stores project source code

while:

    ~/.m2/repository
       ↓
    Stores Maven artifacts and dependencies locally

Maven does not use the local repository as a replacement for Git or GitHub.

---

# Key Points

- The local repository is stored on the developer's machine.
- Default location is `~/.m2/repository`.
- It stores dependencies, plugins, and locally installed artifacts.
- `mvn install` installs the project's artifact into the local repository.
- Maven can reuse locally available dependencies instead of downloading them again.
- `target/` contains build output, while `.m2/repository/` stores Maven artifacts.
- The local repository is separate from a Git/GitHub source-code repository.

---

# Interview Questions

### What is the Maven local repository?

It is a local directory where Maven stores downloaded dependencies, plugins, and locally installed artifacts.

### Where is the Maven local repository located?

By default:

    ~/.m2/repository

On Windows:

    C:\Users\<username>\.m2\repository

### What does `mvn install` do?

It installs the project's generated artifact into the local Maven repository.

### What is the difference between `target` and `.m2/repository`?

`target` contains the current project's generated build output, while `.m2/repository` contains Maven artifacts and dependencies available to Maven locally.

### Can one local Maven project use another local project's artifact?

Yes. After the artifact has been installed using `mvn install`, another Maven project can use it as a dependency.

### Does Maven download a dependency every time?

No. Maven normally reuses an artifact already available in the local repository if the required version is present.
