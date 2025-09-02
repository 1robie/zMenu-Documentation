---
icon: square-check
---

# Using MenuItemStack

`MenuItemStack` is a utility class in zMenu that allows you to define and reuse item representations (name, lore, material, etc.) from configuration files.

In this guide, you'll learn how to load and build `MenuItemStack` objects.

***

## Step 1: Load a MenuItemStack

There are two ways to load a `MenuItemStack` using the `InventoryManager`.

#### From a YamlConfiguration

```java
MenuItemStack itemStack = inventoryManager.loadItemStack(configuration, "path.to.item", file);
```

* `configuration`: A `YamlConfiguration` instance
* `"path.to.item"`: Path to the section in the YAML
* `file`: The file source (for error tracking)

#### From a Map (programmatic)

```java
MenuItemStack itemStack = inventoryManager.loadItemStack(file, "path", map);
```

* `map`: A `Map<String, Object>` that contains the item configuration
* `file`: Source file
* `"path"`: Identifier path used for context

***

## Step 2: Build the ItemStack

Once loaded, you can build the final `ItemStack` using one of the following methods:

```java
ItemStack stack = itemStack.build(player);
```

Or with additional options:

```java
ItemStack stack = itemStack.build(player, true);
```

```java
Placeholders placeholders = new Placeholders();
placeholders.register("key", "value");
ItemStack stack = itemStack.build(player, true, placeholders);
```

* `player`: The player the item is built for (can be used for placeholders)
* `useCache`: Set to false if you want to force rebuild instead of cached copy
* `placeholders`: Optional dynamic values to insert in name/lore

***

## Example YAML

```yaml
example-item:
  material: DIAMOND
  name: "&bSpecial Item"
  lore:
    - "&7This item is amazing"
    - "&f%player_name% will love it!"
```

You can load this item using:

```java
MenuItemStack item = inventoryManager.loadItemStack(configuration, "example-item", file);
```

And then:

```java
ItemStack built = item.build(player);
```

***

## Result

You now have a reusable, customizable item system that supports placeholders, dynamic building, and centralized configuration.

This is especially useful for:

* Reward items
* Display icons
* Buttons
* Static items in menus
