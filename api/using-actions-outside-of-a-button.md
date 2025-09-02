---
description: >-
  zMenu actions are not limited to button clicks — you can execute them
  independently in your own plugin logic. This is useful for reusing features
  like sending messages, teleporting, executing commands
icon: hexagon-check
---

# Using Actions Outside of a Button

## Step 1: Load Actions from Configuration

First, retrieve a list of maps from your plugin’s configuration:

```java
List<Map<String, Object>> rawActions = config.getMapList("custom-actions");
```

Example in `config.yml`:

```yaml
custom-actions:
  - type: console command
    commands:
      - "eco give %player% 1000 %reason%"
```

***

## Step 2: Load Action Instances

Use the `ButtonManager` to convert this list into a list of executable `Action` instances:

```java
List<Action> actions = buttonManager.loadActions(rawActions, "custom-actions", configFile);
```

* `rawActions`: The list from the configuration
* `"custom-actions"`: Used for error context
* `configFile`: The File object from which the config was loaded

***

## Step 3: Prepare Execution Context

To execute actions, you need a `Player`, a fake `InventoryEngine`, and an optional `Placeholders` object.

```java
InventoryEngine inventory = inventoryManager.getFakeInventory();
Placeholders placeholders = new Placeholders();
placeholders.register("reason", "Nice player");
```

You can add as many placeholders as needed using:

```java
placeholders.register("key", "value");
```

***

## Step 4: Execute the Actions

Loop through each action and call:

```java
for (Action action : actions) {
    action.preExecute(player, null, inventory, placeholders);
}
```

* `player`: The target player
* `null`: No button is involved, so this can be null
* `inventory`: A fake inventory engine
* `placeholders`: Your placeholder context

***

### Use Case Examples

* Reward players when they complete an achievement
* Run predefined logic when joining the server
* Trigger effects on custom events

### Result

You've now reused zMenu's powerful action system in your own logic — fully integrated and dynamic!

