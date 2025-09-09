---
description: >-
  In this section, you'll learn how to define a custom action that can be
  triggered by a button or a condition.
icon: square-check
---

# Creating a Custom Action

### Goal

We want to define an action that sends a message to the player. This action can be linked to a button click or to permission success/failure.

### Step 1: Create the Action Class

Create a class that extends `Action`:

```java
import fr.maxlego08.menu.api.button.Button;
import fr.maxlego08.menu.api.engine.InventoryEngine;
import fr.maxlego08.menu.api.requirement.Action;
import fr.maxlego08.menu.api.utils.Placeholders;
import net.kyori.adventure.text.Component;
import org.bukkit.entity.Player;

public class ExampleAction extends Action {

    @Override
    protected void execute(Player player, Button button, InventoryEngine inventoryEngine, Placeholders placeholders) {
        player.sendMessage(Component.text("You clicked on me"));
    }
}
```

This action simply sends a message when executed.

### Step 2: Create an Action Loader

The loader defines how the action is loaded and which identifier it uses in the configuration.

```java
import fr.maxlego08.example.actions.ExampleAction;
import fr.maxlego08.menu.api.loader.ActionLoader;
import fr.maxlego08.menu.api.requirement.Action;
import fr.maxlego08.menu.api.utils.TypedMapAccessor;

import java.io.File;

public class ExampleActionLoader extends ActionLoader {

    public ExampleActionLoader() {
        super("example-action", "example action");
    }

    @Override
    public Action load(String path, TypedMapAccessor accessor, File file) {
        return new ExampleAction();
    }
}
```

### Step 3: Register the Action Loader

Inside your `onEnable()` method:

```java
buttonManager.registerAction(new ExampleActionLoader());
```

### Step 4: Use It in an Inventory or Permission

Example usage in an inventory:

```yaml
basic:
  type: BASIC_EXAMPLE
  slot: 10
  key-example: basic
  item:
    material: DIAMOND
    name: "&7Basic"
  actions:
    - example-action
```

The action will be triggered when the button is clicked.

### Result

Clicking the button will display:

```
You clicked on me
```
