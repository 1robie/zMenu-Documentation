# ℹ️ Getting Started with zMenu API

This tutorial will guide you through creating a plugin using the [zMenu API](https://github.com/Maxlego08/zMenu), a powerful system to create advanced and dynamic inventory menus for Minecraft servers.

### Requirements

* Java 21+
* Spigot or Paper (1.20.4+ recommended)
* Basic knowledge of plugin development

### Installation

To use the zMenu API in your plugin, you need to add the repository and dependency to your build system.

#### Maven

Add the repository:

```xml
<repositories>
  <repository>
    <id>groupez</id>
    <url>https://repo.groupez.dev/releases</url>
  </repository>
</repositories>
```

Add the dependency:

```xml
<dependencies>
  <dependency>
    <groupId>fr.maxlego08.menu</groupId>
    <artifactId>zmenu-api</artifactId>
    <version>1.1.0.0</version>
    <scope>provided</scope>
  </dependency>
</dependencies>
```

#### Gradle Kotlin DSL

Add the repository:

```kotlin
repositories {
    maven {
        name = "groupez"
        url = uri("https://repo.groupez.dev/releases")
    }
}
```

Add the dependency:

```kotlin
dependencies {
    compileOnly("fr.maxlego08.menu:zmenu-api:1.1.0.0")
}
```

#### Gradle Groovy DSL

Add the repository:

```groovy
repositories {
    maven {
        name "groupez"
        url "https://repo.groupez.dev/releases"
    }
}
```

Add the dependency:

```groovy
dependencies {
    compileOnly "fr.maxlego08.menu:zmenu-api:1.1.0.0"
}
```

### Snapshots

If you want to test development versions, replace `releases` by `snapshots` in the repository URL:

* `https://repo.groupez.dev/snapshots`
