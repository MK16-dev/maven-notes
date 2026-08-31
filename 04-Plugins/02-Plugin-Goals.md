# Maven Plugin Goals

A plugin goal is a specific task provided by a Maven plugin.

A Maven plugin can contain multiple goals, with each goal performing a particular operation.

---

## Basic Syntax

A plugin goal can be executed using:

    mvn plugin-prefix:goal

Example:

    mvn exec:java

Here:

    exec → plugin prefix
    java → goal

---

## Common Examples

### Compile

The Maven Compiler Plugin provides the `compile` goal.

    mvn compiler:compile

It compiles the project's Java source code.

### Test

The Maven Surefire Plugin provides the `test` goal.

    mvn surefire:test

It runs the project's tests.

### Clean

The Maven Clean Plugin provides the `clean` goal.

    mvn clean:clean

It removes the build output directory.

### Dependency Tree

The Maven Dependency Plugin provides the `tree` goal.

    mvn dependency:tree

It displays the project's dependency hierarchy.

### Execute Java Application

The Exec Maven Plugin provides the `java` goal.

    mvn exec:java -Dexec.mainClass=com.example.App

It runs the specified Java class.

---

## Plugin Prefix

A plugin prefix is a short name used to execute a plugin.

For example:

    mvn exec:java

Here:

    exec → plugin prefix
    java → plugin goal

The full plugin is:

    org.codehaus.mojo:exec-maven-plugin

---

## Goal with a Lifecycle Phase

Maven can execute lifecycle phases and plugin goals together.

Example:

    mvn clean package

Here:

    clean   → lifecycle phase
    package → lifecycle phase

Maven executes the required plugin goals associated with those phases.

---

## Multiple Goals

Multiple plugin goals can also be executed in one command.

Example:

    mvn clean compiler:compile

Maven first runs the clean goal and then the compiler goal.

---

## Goal Parameters

Some plugin goals require configuration or parameters.

Example:

    mvn exec:java -Dexec.mainClass=com.example.App

Here:

    exec:java → plugin goal
    exec.mainClass → parameter
    com.example.App → parameter value

---

## Plugin Goal vs Lifecycle Phase

These are related but different concepts.

### Lifecycle Phase

A predefined stage of the Maven build lifecycle.

Examples:

    validate
    compile
    test
    package
    install
    deploy

### Plugin Goal

A specific task provided by a plugin.

Examples:

    compiler:compile
    surefire:test
    dependency:tree
    exec:java

The relationship can be represented as:

    Lifecycle Phase
          ↓
    Plugin Goal

---

## Key Points

- A plugin goal performs a specific task.
- Goals are executed using `plugin-prefix:goal`.
- A plugin can provide multiple goals.
- Goals can be executed directly or through lifecycle phases.
- Parameters can be passed using `-D`.
- Example:

      mvn exec:java -Dexec.mainClass=com.example.App

- Lifecycle phases and plugin goals are different concepts.

---

## Summary

A Maven plugin provides functionality, while a plugin goal represents a specific task provided by that plugin.

The general format is:

    mvn plugin-prefix:goal

Example:

    mvn dependency:tree

This executes the `tree` goal of the Dependency Maven Plugin.
