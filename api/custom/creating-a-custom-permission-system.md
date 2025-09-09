---
description: >-
  In this section, you'll learn how to implement a custom permission system
  using zMenu's Permissible class.
icon: square-check
---

# Creating a Custom Permission System

## Goal

We want to define custom permission logic that determines whether a button can be interacted with. If the player has permission, a success action is executed; otherwise, a deny action is triggered.

### Step 1: Create the Permissible Class

```java
import fr.maxlego08.menu.api.button.Button;
import fr.maxlego08.menu.api.engine.InventoryEngine;
import fr.maxlego08.menu.api.requirement.Action;
import fr.maxlego08.menu.api.requirement.Permissible;
import fr.maxlego08.menu.api.utils.Placeholders;
import org.bukkit.entity.Player;

import java.util.List;

public class ExamplePermissible extends Permissible {

    public ExamplePermissible(List<Action> denyActions, List<Action> successActions) {
        super(denyActions, successActions);
    }

    @Override
    public boolean hasPermission(Player player, Button button, InventoryEngine inventoryEngine, Placeholders placeholders) {
        // Custom logic, always allows in this example
        return true;
    }

    @Override
    public boolean isValid() {
        return true;
    }
}
```

### Step 2: Create a Loader for It

```java
import fr.maxlego08.example.permissibles.ExamplePermissible;
import fr.maxlego08.menu.api.ButtonManager;
import fr.maxlego08.menu.api.loader.PermissibleLoader;
import fr.maxlego08.menu.api.requirement.Action;
import fr.maxlego08.menu.api.requirement.Permissible;
import fr.maxlego08.menu.api.utils.TypedMapAccessor;

import java.io.File;
import java.util.List;

public class ExamplePermissibleLoader extends PermissibleLoader {

    private final ButtonManager buttonManager;

    public ExamplePermissibleLoader(ButtonManager buttonManager) {
        super("example-permissible");
        this.buttonManager = buttonManager;
    }

    @Override
    public Permissible load(String path, TypedMapAccessor accessor, File file) {
        List<Action> denyActions = this.loadAction(this.buttonManager, accessor, "deny", path, file);
        List<Action> successActions = this.loadAction(this.buttonManager, accessor, "success", path, file);
        return new ExamplePermissible(denyActions, successActions);
    }
}
```

### Step 3: Register the Permissible Loader

Inside your plugin’s `onEnable()` method:

```java
buttonManager.registerPermissible(new ExamplePermissibleLoader(buttonManager));
```

### Step 4: Use It in Your Configuration

In a YAML inventory file:

```yaml
basic:
  type: BASIC_EXAMPLE
  slot: 10
  key-example: basic
  item:
    material: DIAMOND
    name: "&7Basic"
  permission:
    type: example-permissible
    success:
      - example-action
    deny:
      - example-action
```

### Result

When the player clicks the button:

* If `hasPermission(...)` returns true → `success` actions are executed.
* Otherwise → `deny` actions are executed.
