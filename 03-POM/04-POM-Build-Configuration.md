# Maven Build Configuration

The `<build>` section in `pom.xml` is used to configure how Maven builds the project.

It can be used to configure:

- Plugins
- Source directories
- Resource directories
- Test source directories
- Output directories
- Final artifact name
- Build-related settings

The basic structure is:

    <build>
        ...
    </build>

---

## Basic Build Structure

Example:

    <build>

        <plugins>
            ...
        </plugins>

    </build>

The `<plugins>` section is commonly used to configure Maven plugins.

---

# Build Directories

Maven follows a standard project structure.

    project/
    ├── src/
    │   ├── main/
    │   │   ├── java/
    │   │   └── resources/
    │   └── test/
    │       ├── java/
    │       └── resources/
    │
    ├── target/
    └── pom.xml

The `target` directory contains files generated during the build.

For example:

    target/
    ├── classes/
    ├── test-classes/
    ├── surefire-reports/
    └── maven-demo-1.0-SNAPSHOT.jar

---

# Source Directory

Maven's default main source directory is:

    src/main/java

This is where the application's Java source code is stored.

Example:

    src/main/java/com/example/App.java

Maven automatically knows this location because it follows Maven's standard project structure.

---

# Test Source Directory

The default test source directory is:

    src/test/java

Test classes are stored here.

Example:

    src/test/java/com/example/AppTest.java

Maven compiles test source code separately from application source code.

---

# Resources Directory

The default main resources directory is:

    src/main/resources

It is commonly used for:

- Configuration files
- Properties files
- XML files
- Other application resources

Example:

    src/main/resources/application.properties

The default test resources directory is:

    src/test/resources

It contains resources required specifically for tests.

---

# Build Output Directory

Maven normally stores generated build files inside:

    target/

For example:

    target/classes/

contains compiled application classes.

    target/test-classes/

contains compiled test classes.

    target/surefire-reports/

contains test reports.

---

# Configuring the Final Artifact Name

The `<finalName>` element can be used to change the name of the generated artifact.

Example:

    <build>
        <finalName>my-application</finalName>
    </build>

Instead of:

    maven-demo-1.0-SNAPSHOT.jar

the packaged artifact can be generated as:

    my-application.jar

---

# Configuring Source and Test Directories

Maven allows directories to be customized.

Example:

    <build>

        <sourceDirectory>src/main/java</sourceDirectory>

        <testSourceDirectory>src/test/java</testSourceDirectory>

    </build>

However, for normal Maven projects, it is recommended to follow the standard directory structure rather than changing these locations unnecessarily.

---

# Build Plugins

Plugins are one of the most important parts of Maven's build configuration.

Example:

    <build>
        <plugins>

            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>3.5.0</version>
            </plugin>

        </plugins>
    </build>

Plugins provide Maven with functionality such as:

- Compiling source code
- Running tests
- Creating JAR/WAR files
- Running Java applications
- Generating reports
- Performing code analysis

Plugins are covered in detail in the `04-Plugins` section.

---

# Build Plugin Configuration

A plugin can contain a `<configuration>` section.

Example:

    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.5.0</version>

        <configuration>
            ...
        </configuration>

    </plugin>

The configuration depends on the plugin being used.

---

# Build Extensions

Maven also supports build extensions through:

    <extensions>

        ...

    </extensions>

Build extensions can modify or extend Maven's build behavior.

They are less commonly required in basic Maven projects.

---

# Our Maven Project

Our current `pom.xml` contains:

    <build>
        <plugins>

            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>3.5.0</version>
            </plugin>

        </plugins>
    </build>

This configuration makes the Exec Maven Plugin available to our project.

We used it with:

    mvn exec:java -Dexec.mainClass=com.example.App

which successfully executed our application.

---

# Build Configuration and Lifecycle

Maven's build configuration works together with the Maven lifecycle.

For example:

    mvn compile

causes Maven to execute the required lifecycle phases and plugins to compile the application.

Similarly:

    mvn test

compiles the project and tests and then runs the tests.

And:

    mvn package

builds and packages the application into an artifact such as a JAR.

---

# `mvn clean`

The `clean` lifecycle removes files generated by previous builds.

We ran:

    mvn clean

and Maven removed:

    target/

The output showed:

    Deleting C:\Users\mital\maven-demo\target

This demonstrates that `target/` contains generated build output and can safely be recreated by Maven.

---

# Standard Build Flow

A typical Maven project follows this process:

    Source Code
        ↓
    Compile
        ↓
    Test
        ↓
    Package
        ↓
    Artifact

For our project:

    src/main/java
        ↓
    target/classes
        ↓
    Tests
        ↓
    target/test-classes
        ↓
    JAR
        ↓
    target/maven-demo-1.0-SNAPSHOT.jar

---

# Why Standard Build Configuration Is Useful

Maven provides sensible defaults.

For example:

    src/main/java
    src/main/resources
    src/test/java
    src/test/resources
    target

Because Maven already knows these locations, a basic project does not require a large amount of configuration.

This is part of Maven's principle of:

    Convention over Configuration

Developers can follow Maven's standard conventions instead of configuring every directory manually.

---

# Key Points

- The `<build>` section configures the Maven build.
- Plugins are configured inside `<build>`.
- `src/main/java` is the default main source directory.
- `src/test/java` is the default test source directory.
- `src/main/resources` contains main application resources.
- `src/test/resources` contains test resources.
- `target/` contains generated build output.
- `<finalName>` can change the generated artifact name.
- Plugin configuration can be placed inside `<plugin>`.
- Maven's standard directory structure reduces configuration.
- Build configuration works together with Maven's lifecycle.

---

# Summary

The `<build>` section is responsible for configuring important aspects of how Maven builds a project.

For a simple project, Maven provides sensible defaults, so only a small amount of configuration may be required.

As projects become more complex, the `<build>` section can be used to configure plugins, artifact names, directories, resources, and other build behavior.
