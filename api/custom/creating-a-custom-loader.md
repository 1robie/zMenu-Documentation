---
description: >-
  In this section, you'll learn how to create a custom loader for your own
  button types.
icon: octagon-check
---

# Creating a Custom Loader

## Goal

We will explain how a custom `ButtonLoader` works by revisiting the `BasicLoader` class used for the `BasicButton`.

> **Note:** This section assumes you already have a custom button class. If not, see [Creating a Basic Button](../create-button.md) for instructions on button creation.

### What Is a Loader?

A loader allows zMenu to load buttons from YAML configuration files dynamically. It maps a custom `type:` to the logic that instantiates the corresponding button.

**Comparison:**
- **Button:** Contains the logic and behavior for your custom button.
- **Loader:** Bridges configuration (YAML) to your button by instantiating it with parameters from the config.

### Step 1: Extend `ButtonLoader`

Here’s a breakdown of the `BasicLoader` implementation:

```java
import fr.maxlego08.example.buttons.BasicButton;
import fr.maxlego08.menu.api.button.Button;
import fr.maxlego08.menu.api.button.DefaultButtonValue;
import fr.maxlego08.menu.api.loader.ButtonLoader;
import org.bukkit.configuration.file.YamlConfiguration;
import org.bukkit.plugin.Plugin;

public class BasicLoader extends ButtonLoader {

    public BasicLoader(Plugin plugin) {
        super(plugin, "BASIC_EXAMPLE");
    }

    @Override
    public Button load(YamlConfiguration configuration, String path, DefaultButtonValue defaultButtonValue) {
        String key = configuration.getString(path + "key-example", "default key");
        return new BasicButton(key);
    }
}
```

#### Constructor Explained

* `super(plugin, "BASIC_EXAMPLE")`: This tells zMenu that this loader is responsible for buttons of type `BASIC_EXAMPLE` in your inventories.

#### Loading Parameters from YAML

This example reads a string from the config using:

```java
String key = configuration.getString(path + "key-example", "default key");
```

You can extract any number of parameters and pass them to your button constructor. For advanced scenarios, you can validate, transform, or handle missing values here.

### Step 2: Register the Loader

You must register the loader inside your plugin’s `onEnable()` method:

```java
buttonManager.register(new BasicLoader(this));
```

Once registered, any button with `type: BASIC_EXAMPLE` will be loaded using your custom logic.

---

## See Also
- [Creating a Basic Button](../create-button.md): Learn how to implement the button logic and behavior.
