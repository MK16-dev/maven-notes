# Maven Snapshot and Release Versions

Maven uses version numbers to identify different versions of an artifact.

Two important types of Maven versions are:

- Snapshot versions
- Release versions

Understanding the difference is important when working with Maven repositories and CI/CD pipelines.

---

## 1. Snapshot Version

A snapshot version represents a version that is still under development.

Example:

    1.0-SNAPSHOT

Our Maven project currently uses:

    <version>1.0-SNAPSHOT</version>

This means the project is considered a development version rather than a final release.

---

## Why Use `SNAPSHOT`?

During development, the code may change frequently.

Instead of creating a new final version every time a change is made, developers can continue using a snapshot version.

For example:

    1.0-SNAPSHOT

can represent the ongoing development of version 1.0.

A snapshot repository can therefore contain updated builds of the same snapshot version.

---

# 2. Release Version

A release version represents a stable version of an artifact.

Examples:

    1.0
    1.1
    2.0

A release is intended to be a finalized version that other projects can depend on.

For example:

    <version>1.0</version>

indicates a release version rather than a snapshot.

---

# Snapshot vs Release

| Snapshot | Release |
|---|---|
| Development version | Stable/final version |
| Ends with `-SNAPSHOT` | Does not normally end with `-SNAPSHOT` |
| Can be updated during development | Intended to remain unchanged |
| Used while development is ongoing | Used for finalized versions |
| Example: `1.0-SNAPSHOT` | Example: `1.0` |

---

# Example Development Flow

A project may start with:

    1.0-SNAPSHOT

Developers continue making changes and publishing snapshot builds.

Once the version is considered stable, a release can be created:

    1.0

Later development can continue as:

    1.1-SNAPSHOT

and eventually become:

    1.1

The flow can look like:

    1.0-SNAPSHOT
          ↓
        1.0
          ↓
    1.1-SNAPSHOT
          ↓
        1.1

---

# Snapshot Repository and Release Repository

Organizations commonly separate snapshot and release artifacts.

For example:

    Snapshot Repository
    → Development versions

    Release Repository
    → Stable versions

A repository manager such as Nexus Repository or JFrog Artifactory can manage these artifacts.

---

# Important Maven Rule

A version ending with:

    -SNAPSHOT

is treated as a snapshot version.

Example:

    2.0-SNAPSHOT

A version without `-SNAPSHOT` is treated as a release version.

Example:

    2.0

---

# Our Maven Project

Our current `pom.xml` contains:

    <version>1.0-SNAPSHOT</version>

Therefore, our project is currently using a snapshot version.

When we previously ran:

    mvn install

Maven installed:

    maven-demo-1.0-SNAPSHOT.jar

into the local repository.

---

# Important Interview Point

A snapshot should not be treated as a final immutable release.

Snapshot versions are useful during active development because newer builds can replace or update the snapshot artifact.

Release versions are intended to represent stable versions that should remain unchanged.

---

# Key Points

- `SNAPSHOT` indicates a development version.
- Example: `1.0-SNAPSHOT`.
- A release version represents a stable version.
- Example: `1.0`.
- Snapshot artifacts may be updated during development.
- Release artifacts are intended to remain stable.
- Snapshot and release artifacts are commonly managed separately in repositories.
- Our Maven project currently uses `1.0-SNAPSHOT`.

---

# Interview Questions

### What is a SNAPSHOT version in Maven?

A SNAPSHOT version represents a development version that may change as development continues.

### What is the difference between `1.0-SNAPSHOT` and `1.0`?

`1.0-SNAPSHOT` is a development version, while `1.0` is a release version intended to be stable.

### Why are SNAPSHOT versions used?

They allow developers to publish and consume ongoing development builds without creating a new release version for every change.

### Can a SNAPSHOT artifact change?

Yes. New builds of the same snapshot version can be published during development.

### Should a release artifact normally be modified after release?

No. Release versions are intended to be stable and should generally remain unchanged.

### What version is our current Maven project using?

    1.0-SNAPSHOT

because the `pom.xml` contains:

    <version>1.0-SNAPSHOT</version>
