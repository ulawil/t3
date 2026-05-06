* Novice
	* [ ] Manually can configure a single module, java plugin, and public repo dependencies usage
	* [ ] Command line usage: build, test
	* [ ] GAV coordinates
* Competent
	* [ ] Understanding: build phases and dependency scopes: runtime, compile, etc
	* [ ] Declare repositories
	* [ ] Java application plugin
	* [ ] Multi-project build
	* [ ] Version constrains
	* [ ] Customizing unit test execution







# Gradle

## Understanding: build phases and dependency scopes: runtime, compile, etc

### Build phases
In gradle there are tasks instead of phases that depend on each other (dependency chain); For example, when running `build`, the task it depends on - `assemble` and `check` will run first

### Dependency scopes
Dependency scopes specifies when the dependency is available and used
- implementation - available at compile and runtime, e.g. `spring-boot-starter` dependencies (`data-jpa`, `security`...)
- compileOnly - only available at compile time and not runtime, e.g. lombok
- runtimeOnly - only available at runtime and not compile time, e.g. 
- annotationProcessor - for tools that generate code based on annotations, e.g. lomgok, mapstruct
- testImplementation - available at test compile and runtime, e.g. `spring-boot-starter-test` dependencies, junit...
- testCompileOnly
- testRuntimeOnly
- testAnnotationProcessor

## Declare repositories
Gradle needs to know where to find declared dependencies, we put repositories in:
```gradle
repositories {
    mavenLocal()
	  mavenCentral()
    maven {
        url = uri(...) // for internal company libraries
    }
}
```
- Repository resolution order - in gradle, in order they're listed

## Java application plugin
- `java` plugin - for compiling and testing java code; provides tasks:
  - `compileJava`
  - `test`
  - `jar`
- `application` plugin - for running code as an app (applies `java` plugin implicitly); provides tasks
  - `run`
  - `installDist`

```gradle
plugins {
	application
}
```

## Version constrains
```gradle
// fixed version
implementation("com.google.guava:guava:33.0.0-jre")

// strict version constraint
implementation("com.google.guava:guava") {
    version {
        strictly("33.0.0-jre")
    }
}

// "at least" version constraint
implementation("com.google.guava:guava") {
    version {
        require("33.0.0-jre")
    }
}

// "soft" constraint which can be overriden by others
implementation("com.google.guava:guava") {
    version {
        prefer("33.0.0-jre")
    }
}

// version range
implementation("com.google.guava:guava:[31,34)")

// dynamic version - automatically picks laterst patch
implementation("com.google.guava:guava:33.+")

```
