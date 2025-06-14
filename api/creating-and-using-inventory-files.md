---
description: >-
  In this section, you'll learn how to define an inventory layout using a YAML
  file and how to load it using zMenu.
icon: octagon-check
---

# Creating and Using Inventory Files

### Goal

We want to define a visual menu using a YAML file and load it at plugin startup.

### Step 1: Create a YAML Inventory File

Create a file named `example.yml` in your `resources/inventories/` folder.

```yaml
name: "&8Example &f%page%&8/&f%max-page%"
size: 18
buttons:

  basic:
    type: BASIC_EXAMPLE
    slot: 10
    key-example: basic
    item:
      material: DIAMOND
      name: "&7Basic"

  pagination:
    type: PAGINATION_EXAMPLE
    slots:
      - 0-8
    item:
      material: BOOK
      name: "&7Book&8: &f%book%"

  next:
    type: NEXT
    slot: 17
    item:
      material: ARROW
      name: "&7Next page"

  previous:
    type: PREVIOUS
    slot: 9
    item:
      material: ARROW
      name: "&7Previous page"
```

#### Explanation

* `name`: The inventory title, with support for placeholders.
* `size`: Total number of slots (must be a multiple of 9).
* `buttons`: Defines each button in the inventory with its configuration.
* `type`: Must match a registered button loader name.

### Step 2: Load the Inventory in Your Plugin

Inside your plugin's `onEnable()` method:

```java
try {
    inventoryManager.loadInventoryOrSaveResource(this, "inventories/example.yml");
} catch (InventoryException exception) {
    exception.printStackTrace();
}
```

This method will either load the file or create a default one if it doesn't exist.

### Step 3: Open the Inventory in Your Code

To open the inventory for a player:

```java
inventoryManager.openInventory("example", player);
```

### Tips

* You can use placeholders in names, lore, and even buttons.
* `PAGINATION_EXAMPLE` buttons can use the `%book%` placeholder per page item.

### Result

The menu defined in `example.yml` will be loaded and available in-game. Buttons and actions defined in previous steps will function automatically.
