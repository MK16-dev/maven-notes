# Maven Repositories

A Maven repository is a location where Maven stores and retrieves project artifacts and dependencies.

Artifacts can include:

- JAR files
- WAR files
- POM files
- Maven plugins
- Other project-related packages

Maven uses repositories to download dependencies and store built artifacts.

---

# Types of Maven Repositories

Maven mainly works with three types of repositories:

1. Local Repository
2. Central Repository
3. Remote Repository

The basic flow is:

    Project
       ↓
    Local Repository
       ↓
    Central / Remote Repository

---

# 1. Local Repository

The local repository is stored on the developer's computer.

On Windows, Maven normally uses:

    C:\Users\<username>\.m2\repository

In Git Bash, it can be accessed using:

    ~/.m2/repository

Our Maven project used this location:

    C:\Users\mital\.m2\repository

---

## Purpose of the Local Repository

Maven uses the local repository to:

- Store downloaded dependencies.
- Store Maven plugins.
- Store artifacts installed using `mvn install`.
- Avoid downloading the same artifact repeatedly.

For example, after running:

    mvn install

our project was stored under:

    ~/.m2/repository/com/example/maven-demo/1.0-SNAPSHOT/

It contained:

    maven-demo-1.0-SNAPSHOT.jar
    maven-demo-1.0-SNAPSHOT.pom

---

# 2. Maven Central Repository

Maven Central is the default public repository used by Maven to download many commonly used dependencies and plugins.

For example, during our Maven build, Maven downloaded artifacts from:

    repo.maven.apache.org

If a required dependency is not available in the local repository, Maven can download it from a configured remote repository such as Maven Central.

---

# 3. Remote Repository

A remote repository is a repository located on another server.

Organizations often use private remote repositories to store their own internal artifacts.

Examples of repository management tools include:

- Nexus Repository
- JFrog Artifactory

A remote repository can be used to share artifacts between developers, teams, or CI/CD systems.

---

# Maven Dependency Resolution

When Maven needs a dependency, it first checks the local repository.

If the required artifact is not available locally, Maven can retrieve it from a configured remote repository.

Conceptually:

    pom.xml
       ↓
    Maven needs dependency
       ↓
    Check Local Repository
       ↓
    Available?
      / \
    Yes  No
     ↓    ↓
    Use  Download from remote repository
              ↓
        Store in Local Repository

This is why dependencies that have already been downloaded are usually available locally for future builds.

---

# Repository Coordinates

Maven identifies artifacts using coordinates such as:

    groupId
    artifactId
    version

Example:

    groupId:    org.apache.commons
    artifactId: commons-lang3
    version:    3.18.0

Maven uses these coordinates to locate the required artifact in a repository.

---

# Local Repository and `mvn install`

When we run:

    mvn install

Maven builds the project and installs its artifact into the local repository.

For our project:

    maven-demo-1.0-SNAPSHOT.jar

was installed under:

    ~/.m2/repository/com/example/maven-demo/1.0-SNAPSHOT/

This allows other local Maven projects to use that artifact as a dependency.

---

# Important Interview Point

The local repository is **not the same as Maven Central**.

### Local Repository

- Exists on your computer.
- Stores downloaded dependencies and locally installed artifacts.
- Usually located under `.m2/repository`.

### Maven Central

- A remote public repository.
- Provides publicly available Maven artifacts.
- Maven can download dependencies from it when they are not already available locally.

---

# Key Points

- A Maven repository stores artifacts and dependencies.
- Local repository is stored on the developer's machine.
- Maven Central is a public remote repository.
- Organizations can maintain private remote repositories.
- `mvn install` places an artifact in the local repository.
- Maven checks the local repository when resolving dependencies.
- Repository coordinates such as `groupId`, `artifactId`, and `version` identify artifacts.

---

# Interview Questions

### What is a Maven repository?

A location where Maven stores and retrieves artifacts such as JARs, POMs, dependencies, and plugins.

### What are the main types of Maven repositories?

- Local repository
- Central repository
- Remote repository

### Where is the Maven local repository located?

By default:

    ~/.m2/repository

On Windows, this normally corresponds to:

    C:\Users\<username>\.m2\repository

### What happens when you run `mvn install`?

Maven builds the project and installs its artifact into the local Maven repository.

### What is Maven Central?

Maven Central is a public remote repository that hosts many Maven dependencies, plugins, and other artifacts.

### Why does Maven use a local repository?

To store downloaded artifacts and locally installed projects, reducing the need to download them again.

### What is the difference between a local and remote repository?

A local repository exists on the developer's machine, while a remote repository exists on a server and can be accessed over a network.
