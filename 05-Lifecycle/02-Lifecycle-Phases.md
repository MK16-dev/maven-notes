# Maven Lifecycle Phases

Maven lifecycle phases represent specific stages in the build process.

The most important phases of the default lifecycle are:

    validate → compile → test → package → verify → install → deploy

---

## 1. Validate

Checks whether the project is correctly configured.

    mvn validate

---

## 2. Compile

Compiles the main Java source code.

    mvn compile

Output:

    target/classes/

For our project:

    src/main/java/com/example/App.java
                ↓
    target/classes/com/example/App.class

---

## 3. Test

Compiles and runs the test code.

    mvn test

Test classes are placed in:

    target/test-classes/

Test reports are placed in:

    target/surefire-reports/

Our project successfully ran:

    Tests run: 1
    Failures: 0
    Errors: 0

---

## 4. Package

Packages the compiled application into an artifact.

    mvn package

For our JAR project, Maven creates:

    target/maven-demo-1.0-SNAPSHOT.jar

---

## 5. Verify

Performs additional checks on the packaged project.

    mvn verify

It is commonly used for additional validation or integration checks.

---

## 6. Install

Installs the generated artifact into the local Maven repository.

    mvn install

The artifact is stored under:

    ~/.m2/repository/

Our project was installed under:

    ~/.m2/repository/com/example/maven-demo/1.0-SNAPSHOT/

---

## 7. Deploy

Deploys the artifact to a remote Maven repository.

    mvn deploy

This is commonly used when publishing artifacts for other developers or projects to use.

---

# Important Concept: Earlier Phases Run First

Maven executes lifecycle phases in order.

For example:

    mvn package

effectively goes through:

    validate
        ↓
    compile
        ↓
    test
        ↓
    package

Similarly:

    mvn install

runs the required phases before `install`.

Therefore, you normally do not need to run every phase separately.

---

# Phase vs Goal

A lifecycle phase:

    package

is different from a plugin goal:

    jar:jar

The phase is part of Maven's lifecycle, while the goal is provided by a plugin.

Example:

    mvn package
         ↓
    Maven lifecycle
         ↓
    Plugin goals execute
         ↓
    JAR is created

---

# Key Points

- Lifecycle phases define stages of the Maven build.
- Important phases are `validate`, `compile`, `test`, `package`, `verify`, `install`, and `deploy`.
- Running a later phase automatically runs the required earlier phases.
- `compile` creates compiled classes.
- `test` runs tests.
- `package` creates the artifact.
- `install` places the artifact in the local repository.
- `deploy` publishes the artifact to a remote repository.

---

# Interview Questions

### What is a Maven lifecycle phase?

A predefined stage in the Maven build process that performs a particular part of the build.

### What happens during the `package` phase?

The project is compiled and tested through the required earlier phases, then packaged into an artifact such as a JAR or WAR.

### What is the difference between `package` and `install`?

`package` creates the artifact, while `install` also places that artifact into the local Maven repository.

### What is the difference between `install` and `deploy`?

`install` puts the artifact in the local repository, while `deploy` publishes it to a remote repository.

### Does `mvn install` run `mvn package` first?

Yes. Maven executes the required earlier lifecycle phases before reaching `install`.
