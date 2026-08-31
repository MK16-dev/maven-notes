# Maven Plugin Management

Plugin management is used to define plugin configuration and versions in one central place so they can be reused consistently.

It is mainly done using:

    <pluginManagement>

---

## `<pluginManagement>` vs `<plugins>`

### `<pluginManagement>`

Defines the default configuration or version for plugins, but **does not activate the plugin by itself**.

### `<plugins>`

Declares plugins that are actually used in the build.

Example:

    <build>

        <pluginManagement>
            <plugins>

                <plugin>
                    <groupId>org.apache.maven.plugins</groupId>
                    <artifactId>maven-compiler-plugin</artifactId>
                    <version>3.15.0</version>
                </plugin>

            </plugins>
        </pluginManagement>

        <plugins>

            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
            </plugin>

        </plugins>

    </build>

Here, `pluginManagement` provides the version, while `<plugins>` activates the plugin.

---

## Why Use `pluginManagement`?

It is especially useful in multi-module Maven projects.

It helps:

- Keep plugin versions consistent.
- Avoid repeating plugin configuration.
- Centralize plugin settings.
- Make project maintenance easier.

---

## Important Interview Point

A common interview question is:

**Does `pluginManagement` execute a plugin?**

**No.**

`pluginManagement` only provides default configuration. The plugin must be declared under `<plugins>` to be used.

---

## Key Points

- `pluginManagement` centralizes plugin configuration.
- It does not activate plugins by itself.
- `<plugins>` is used to activate plugins.
- It is particularly useful in multi-module projects.
- It helps maintain consistent plugin versions and configuration.
