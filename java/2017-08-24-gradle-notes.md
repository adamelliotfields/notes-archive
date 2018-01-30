# Gradle Notes
:calendar: *August 24, 2017*

Gradle is an open source build automation system that uses a Groovy-based DSL instead of XML for
declaring project configuration.

### Projects and Tasks
Every Gradle build is made up of one or more projects. A project might represent a library JAR or a
web application. A project might also represent an action, like deploying an application.

Each project is made up of one or more tasks. A task represents some atomic piece of work for Gradle
to perform. Tasks could be compiling Java classes or creating a JAR.

### Initializing a Project
Running the `gradle init` command will create all the necessary starter files for a Gradle build,
including a standalone Gradle binary.

Gradle also has a `--type` flag to specify the build init type. This will pre-configure the
`build.gradle` configuration and also generate the appropriate project folder structure.

##### Java Application
The Application plugin facilitates creating an executable JVM application. Applying the application
plugin implicitly applies the Java plugin as well.

The build task will generate ZIP and TAR archives that include a binary and Windows batch file.

```bash
gradle init --type java-application
```

See the Gradle
[docs](https://docs.gradle.org/current/userguide/build_init_plugin.html#sec:build_init_types) for
more build init types.

### Importing Project to IntelliJ
To activate the Gradle tool window in IntelliJ, you must import the project or module as a Gradle
project or module.

### Project Structure
Gradle uses the same structure as Maven for source and test files.

Compiled builds will be output to the `build` folder (in Maven this is the `target` folder).

### `build.gradle`
The Gradle build script defines a project and its tasks, as well as repositories for resolving
dependencies (and what those dependencies are).

This is the generated build script from the `java-application` build init type:

```groovy
apply plugin: 'java'
apply plugin: 'application'

repositories {
  jcenter()
}

dependencies {
  compile 'com.google.guava:guava:22.0'

  testCompile 'junit:junit:4.12'
}

mainClassName = 'App'
```

Be sure to adjust `mainClassName` to reflect the package name.

Note that you'll have to manually add your group and version number to the top of your build script:

```groovy
group 'io.github.adamelliotfields'
version '1.0.0'
```

### `settings.gradle`
Before Gradle assembles the project for a build, it creates a `Settings` instance based on the
properties in the `settings.gradle` file.

By default, only the `rootProject` is defined. In multi-project builds, additional projects may be
defined.

```groovy
rootProject.name 'my-app'
```
