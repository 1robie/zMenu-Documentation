---
description: In this section, you'll learn how to create a basic custom button using zMenu.
icon: hexagon-check
---

# Creating a Basic Button

## Goal

We will create a button that sends a message to the player when clicked. The button is registered with the name `BASIC_EXAMPLE`.

> **Note:** To use your button in inventories, you also need a loader. See [Creating a Custom Loader](custom/creating-a-custom-loader.md) for details on loader creation and advanced configuration.

### Step 1: Create the Button Class

Create a class `BasicButton` that extends `Button`:

```java
import fr.maxlego08.menu.api.button.Button;
import fr.maxlego08.menu.api.engine.InventoryEngine;
import fr.maxlego08.menu.api.utils.Placeholders;
import net.kyori.adventure.text.Component;
import org.bukkit.entity.Player;
import org.bukkit.event.inventory.InventoryClickEvent;

public class BasicButton extends Button {

    private final String key;

    public BasicButton(String key) {
        this.key = key;
    }

    @Override
    public void onClick(Player player, InventoryClickEvent event, InventoryEngine inventory, int slot, Placeholders placeholders) {
        super.onClick(player, event, inventory, slot, placeholders);
        player.sendMessage(Component.text("Hey, it's nice to meet you! Button key: ").append(Component.text(key)));
    }

    @Override
    public boolean isPermanent() {
        return true;
    }
}
```

### Step 2: Create a Loader (Overview)

A loader allows zMenu to instantiate your button from a configuration file. It bridges your button logic with YAML configuration, enabling dynamic button creation.

> For a full implementation, advanced usage, and parameter extraction, see [Creating a Custom Loader](custom/creating-a-custom-loader.md).

### Step 3: Register the Loader

In your plugin’s `onEnable()` method, register the loader:

```java
buttonManager.register(new BasicLoader(this));
```

### Step 4: Use It in an Inventory

Example usage in `inventories/example.yml`:

```yaml
basic:
  type: BASIC_EXAMPLE
  slot: 10
  key-example: basic
  item:
    material: DIAMOND
    name: "&7Basic"
```

### Result

When a player clicks the button, they will receive a message like:

```
Hey, it's nice to meet you! Button key: basic
```

---

## See Also
- [Creating a Custom Loader](custom/creating-a-custom-loader.md): Learn how to map configuration to your button logic and handle advanced loading scenarios.
