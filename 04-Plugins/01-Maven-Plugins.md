# Maven Plugins

Maven plugins are used to perform specific tasks during the Maven build process.

Maven itself provides the build framework, while plugins provide the functionality needed to perform build tasks.

Examples of tasks performed by plugins:

- Compiling Java code
- Running tests
- Creating JAR/WAR files
- Running Java applications
- Cleaning the project
- Generating reports

---

## Plugin Structure

A Maven plugin is identified using:

- `groupId`
- `artifactId`
- `version`

Example:

    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.5.0</version>
    </plugin>

---

# Plugins in `pom.xml`

Plugins are normally configured inside the `<build>` section:

    <build>
        <plugins>

            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>3.5.0</version>
            </plugin>

        </plugins>
    </build>

---

# Maven Plugin vs Dependency

Plugins and dependencies have different purposes.

### Dependency

A dependency is a library required by the application.

Example:

    commons-lang3

It provides classes such as:

    StringUtils

### Plugin

A plugin performs a Maven build-related task.

Example:

    maven-compiler-plugin

It compiles Java source code.

In simple terms:

    Dependency → Used by the application

    Plugin → Used by Maven during the build

---

# Common Maven Plugins

Some commonly used Maven plugins are:

| Plugin | Purpose |
|---|---|
| `maven-clean-plugin` | Cleans the project |
| `maven-compiler-plugin` | Compiles Java source code |
| `maven-surefire-plugin` | Runs unit tests |
| `maven-jar-plugin` | Creates JAR files |
| `maven-install-plugin` | Installs artifacts into the local repository |
| `maven-deploy-plugin` | Deploys artifacts to a remote repository |
| `exec-maven-plugin` | Executes external commands or Java applications |

---

# Exec Maven Plugin

We used the Exec Maven Plugin in our Maven project.

Configuration:

    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.5.0</version>
    </plugin>

We used it to run our Java application:

    mvn exec:java -Dexec.mainClass=com.example.App

Our application successfully produced:

    true
    MAVEN

This confirmed that the plugin was correctly configured and the application executed through Maven.

---

# Plugin Goals

A plugin can provide one or more goals.

A goal represents a specific task provided by a plugin.

The general command format is:

    mvn plugin-prefix:goal

Example:

    mvn exec:java

Here:

    exec → plugin prefix

    java → plugin goal

Another example:

    mvn dependency:tree

Here:

    dependency → plugin prefix

    tree → plugin goal

---

# Plugin Configuration

Plugin behavior can be customized using the `<configuration>` element.

Example:

    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.5.0</version>

        <configuration>
            ...
        </configuration>

    </plugin>

The configuration options depend on the specific plugin.

---

# Plugins and Maven Lifecycle

Many Maven lifecycle phases are implemented using plugins.

For example:

    mvn compile

uses the Maven Compiler Plugin to compile Java source code.

Similarly:

    mvn test

uses the Maven Surefire Plugin to run tests.

And:

    mvn package

can use the Maven JAR Plugin to create a JAR file.

So the relationship is:

    Maven Lifecycle
          ↓
    Lifecycle Phase
          ↓
    Plugin
          ↓
    Plugin Goal

---

# Key Points

- Maven plugins perform build-related tasks.
- Plugins are configured inside `<build>`.
- Plugins are different from application dependencies.
- A plugin can contain multiple goals.
- Goals can be executed using `mvn plugin:goal`.
- Plugin behavior can be customized using `<configuration>`.
- Maven lifecycle phases are associated with plugin goals.
- `exec-maven-plugin` was used in our project to run the Java application.

---

# Summary

Maven plugins provide the functionality that Maven uses to perform build tasks.

They handle operations such as compiling code, running tests, creating artifacts, cleaning the project, and executing applications.

The basic structure is:

    Maven
      ↓
    Lifecycle Phase
      ↓
    Plugin
      ↓
    Goal
