# Maven Plugin Execution

Plugin execution defines when and how a Maven plugin goal runs during the Maven lifecycle.

A plugin can be connected to a specific lifecycle phase using an `<execution>` block.

---

## Basic Structure

    <plugin>
        <groupId>...</groupId>
        <artifactId>...</artifactId>
        <version>...</version>

        <executions>
            <execution>

                <id>...</id>

                <phase>...</phase>

                <goals>
                    <goal>...</goal>
                </goals>

            </execution>
        </executions>

    </plugin>

---

## Important Elements

### `<executions>`

Contains one or more plugin executions.

### `<execution>`

Defines one specific execution of the plugin.

### `<id>`

Provides a unique name for the execution.

Example:

    <id>run-app</id>

### `<phase>`

Specifies the Maven lifecycle phase to which the execution is bound.

Example:

    <phase>package</phase>

### `<goals>`

Specifies which plugin goal should run.

Example:

    <goals>
        <goal>...</goal>
    </goals>

---

# Example

    <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>exec-maven-plugin</artifactId>
        <version>3.5.0</version>

        <executions>
            <execution>

                <id>run-app</id>

                <phase>package</phase>

                <goals>
                    <goal>java</goal>
                </goals>

                <configuration>
                    <mainClass>com.example.App</mainClass>
                </configuration>

            </execution>
        </executions>

    </plugin>

In this example, the `java` goal is bound to the `package` phase.

Therefore, when the appropriate lifecycle is executed, Maven can run the configured goal automatically.

---

# Direct Goal vs Lifecycle-Bound Goal

A plugin goal can be executed directly:

    mvn exec:java -Dexec.mainClass=com.example.App

Or it can be bound to a lifecycle phase through `<executions>`.

For example:

    <phase>package</phase>

    <goal>java</goal>

Then the goal becomes part of that lifecycle execution.

---

# Why Use Plugin Executions?

Plugin executions are useful when a task should happen automatically as part of a Maven build.

For example:

    mvn package

can automatically trigger a configured plugin goal.

This is useful for tasks such as:

- Code generation
- Running additional checks
- Creating reports
- Running custom build tasks

---

# Key Points

- Plugin execution controls when a plugin goal runs.
- `<executions>` contains plugin executions.
- `<execution>` defines one execution.
- `<phase>` binds the execution to a lifecycle phase.
- `<goals>` specifies the plugin goal.
- `<id>` identifies the execution.
- Plugin goals can be run directly or automatically through lifecycle binding.

---

# Interview Questions

### What is plugin execution in Maven?

It defines when and how a plugin goal should execute during the Maven lifecycle.

### What is the purpose of `<phase>`?

It binds a plugin execution to a specific Maven lifecycle phase.

### What is the purpose of `<goals>`?

It specifies which plugin goal should be executed.

### What is the difference between `mvn plugin:goal` and plugin execution?

`mvn plugin:goal` directly invokes a plugin goal from the command line, while an `<execution>` can bind the goal to a lifecycle phase so it runs automatically as part of that lifecycle.
