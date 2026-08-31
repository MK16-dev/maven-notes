# Maven Properties

Maven properties are key-value pairs used to store reusable values in the `pom.xml` file.

They help keep the POM clean, consistent, and easier to maintain.

---

## Why Use Properties?

Properties are useful when the same value needs to be used in multiple places.

For example, instead of writing the Java version multiple times, we can define it once:

    <properties>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

Maven can then use these values wherever required.

---

# Basic Syntax

Properties are defined inside:

    <properties>
        ...
    </properties>

Example:

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

A property can be referenced using:

    ${property-name}

For example:

    ${maven.compiler.source}

---

# Custom Properties

We can create our own properties.

Example:

    <properties>
        <java.version>21</java.version>
    </properties>

The property can then be referenced as:

    ${java.version}

This is useful when the same value is required in multiple configurations.

---

# Example with Dependency Version

A dependency version can also be stored in a property.

Example:

    <properties>
        <commons-lang3.version>3.18.0</commons-lang3.version>
    </properties>

Then:

    <dependency>
        <groupId>org.apache.commons</groupId>
        <artifactId>commons-lang3</artifactId>
        <version>${commons-lang3.version}</version>
    </dependency>

Now, if the dependency version needs to be changed, we only need to update the property.

---

# Example with Java Version

Instead of directly specifying the Java version in plugin configuration:

    <plugin>
        ...
        <configuration>
            <source>21</source>
            <target>21</target>
        </configuration>
    </plugin>

We can use a property:

    <properties>
        <maven.compiler.source>21</maven.compiler.source>
        <maven.compiler.target>21</maven.compiler.target>
    </properties>

This keeps configuration centralized.

---

# Common Maven Properties

Maven provides several built-in project properties.

Examples include:

    ${project.groupId}
    ${project.artifactId}
    ${project.version}
    ${project.name}
    ${project.packaging}

For our project:

    ${project.groupId}
    
would resolve to:

    com.example

And:

    ${project.artifactId}

would resolve to:

    maven-demo

---

# Project Directory Properties

Maven also provides properties related to project directories.

Examples:

    ${project.basedir}
    ${project.build.directory}
    ${project.build.sourceDirectory}
    ${project.build.testSourceDirectory}

For example:

    ${project.basedir}

represents the project's base directory.

For our project, this is approximately:

    C:\Users\mital\maven-demo

---

# Build Directory

The property:

    ${project.build.directory}

represents the build output directory.

For a standard Maven project, this is:

    target

So:

    ${project.build.directory}

typically resolves to the project's:

    target/

directory.

---

# Source Directory

The standard Java source directory is:

    ${project.build.sourceDirectory}

which normally points to:

    src/main/java

The test source directory is:

    ${project.build.testSourceDirectory}

which normally points to:

    src/test/java

---

# Environment Variables

Maven can also access environment variables using:

    ${env.VARIABLE_NAME}

Example:

    ${env.JAVA_HOME}

This allows Maven configuration to use values from the operating system environment.

---

# System Properties

Maven can also use Java system properties.

For example:

    ${user.home}

can represent the current user's home directory.

System properties can also be supplied from the command line.

Example:

    mvn package -DskipTests=true

Here:

    skipTests

is supplied as a system property.

---

# Command-Line Properties

Properties can be passed to Maven using the `-D` option.

Example:

    mvn package -DskipTests=true

Another example:

    mvn test -Dtest=AppTest

The value can then be used by Maven plugins or project configuration.

---

# Property Naming

It is a good practice to use clear and descriptive property names.

Examples:

    <java.version>21</java.version>

    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>

    <commons-lang3.version>3.18.0</commons-lang3.version>

Avoid unclear names such as:

    <v1>21</v1>

Clear names make the POM easier to understand and maintain.

---

# Example POM Using Properties

Example:

    <project>

        <modelVersion>4.0.0</modelVersion>

        <groupId>com.example</groupId>
        <artifactId>maven-demo</artifactId>
        <version>1.0-SNAPSHOT</version>

        <properties>
            <maven.compiler.source>21</maven.compiler.source>
            <maven.compiler.target>21</maven.compiler.target>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <commons-lang3.version>3.18.0</commons-lang3.version>
        </properties>

        <dependencies>

            <dependency>
                <groupId>org.apache.commons</groupId>
                <artifactId>commons-lang3</artifactId>
                <version>${commons-lang3.version}</version>
            </dependency>

        </dependencies>

    </project>

Here, the Commons Lang version is maintained in one place.

---

# Advantages of Maven Properties

Using properties provides several benefits:

- Avoids repeating values.
- Makes the POM easier to read.
- Makes version updates easier.
- Keeps configuration centralized.
- Reduces the possibility of inconsistent values.
- Makes large Maven projects easier to maintain.

---

# Important Syntax

Property definition:

    <properties>
        <java.version>21</java.version>
    </properties>

Property reference:

    ${java.version}

Command-line property:

    mvn package -DskipTests=true

Environment variable:

    ${env.JAVA_HOME}

Project property:

    ${project.version}

---

# Key Points

- Maven properties store reusable configuration values.
- Properties are defined inside `<properties>`.
- Properties are referenced using `${property-name}`.
- Custom properties can be created by the developer.
- Dependency versions can be stored as properties.
- Maven provides predefined project properties.
- Environment variables can be accessed using `${env.VARIABLE_NAME}`.
- System properties can be supplied using the `-D` option.
- Properties help keep `pom.xml` clean and maintainable.

---

# Summary

Maven properties provide a simple way to define reusable values in `pom.xml`.

Instead of repeatedly writing the same value, define it once:

    <properties>
        <java.version>21</java.version>
    </properties>

and reference it wherever required:

    ${java.version}

This makes Maven configuration more organized, consistent, and easier to maintain.
