---
description: >-
  In this section, you'll learn how to define a custom material loader. This is
  useful if you want to dynamically generate items that aren't just simple
  Material.valueOf(...) items.
icon: hexagon-check
---

# Creating a Custom Material Loader

### Goal

We will create a material loader that always returns a `DIAMOND` item, regardless of the input.

### Step 1: Create the Material Loader Class

Create a class that extends `MaterialLoader`:

```java
import fr.maxlego08.menu.api.loader.MaterialLoader;
import org.bukkit.Material;
import org.bukkit.configuration.file.YamlConfiguration;
import org.bukkit.entity.Player;
import org.bukkit.inventory.ItemStack;

public class ExampleMaterialLoader extends MaterialLoader {

    public ExampleMaterialLoader() {
        super("example-material");
    }

    @Override
    public ItemStack load(Player player, YamlConfiguration yamlConfiguration, String path, String materialString) {
        return new ItemStack(Material.DIAMOND);
    }
}
```

### Constructor Explained

* `super("example-material")`: Registers this loader under the identifier `example-material`. You will use this value in the `material:` field in YAML.

### Step 2: Register the Material Loader

In your plugin’s `onEnable()` method:

```java
inventoryManager.registerMaterialLoader(new ExampleMaterialLoader());
```

### Step 3: Use It in a Configuration

You can now reference your custom material type like this:

```yaml
example-item:
  material: "example-material:hey"
  name: "&fExample Item"
  lore:
    - "&fThis is an example item"
    - "&fYou can use it to test zMenu"
```

### Result

Every time the `example-material` string is encountered in the config, a diamond item will be returned.
