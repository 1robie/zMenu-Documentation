---
description: >-
  The requirements feature allows you to perform actions based on a permission
  check.
---

# 🏁 Requirements

## Requirements

### Syntax

```yaml
# open-requirement
# click-requirement
view-requirement:

  # Set the minimum number of requirements to be able to say this is a success.
  # By default the value will be the same as the number of requirements.
  minimum-requirement: <number>
  
  # List of requirements, all information about each type below
  requirements:
    - type: permission
      permission: "example.permission"
      deny:
        - type: message
          messages:
            - "&cYou don't have permission !"
    - type: placeholder
      placeholder: "%player_gamemode%" # need PAPI ecloud Player
      value: "CREATIVE"    
      action: equals_string
      # Specific deny actions
      deny:
        - type: message
          messages:
            - "&cYou mus be in creative"      
    - type: regex
      input: "%player_item_in_hand%" # need PAPI ecloud Player
      regex: "(NETHERITE_|DIAMOND_|IRON_|GOLDEN_|STONE_|WOODEN_|LEATHER_|BOW|CROSSBOW|FISHING_ROD|SHEARS|SHIELD|TRIDENT|TURTLE_HELMET|ELYTRA|FLINT_AND_STEEL)"      
      deny:
        - type: message
          messages:
            - "&cYou dont have items in your hand !"
  
  # Global Success actions
  success:
    - type: sound
      sound: ENTITY_PLAYER_LEVELUP
      
  # Global Deny actions
  deny:    
    - type: message
      messages:
        - "&cYou doesn't have an item in your hand."
```

In addition to global deny and success actions, you can define specific deny and success actions for each requirement.

### View Requirement

Defines the requirements a player must meet to see a button in the inventory.

#### Example:

```yaml
view-requirement:
  deny:
    - type: chat
      messages:
        - "Hey, my name is %player%"
  success:
    - type: sound
      sound: ENTITY_PLAYER_LEVELUP
  requirements:
    - type: permission
      permission: "admin.use"
    - type: placeholder
      placeholder: "%player_is_flying%"
      value: "yes"
      action: equals_string
```

### Open Requirement

Defines the requirements a player must meet to open the inventory.

#### Example

```yaml
open-requirement:
  requirements:
    - type: regex
      input: "%player_item_in_hand%"
      regex: "(NETHERITE_|DIAMOND_|IRON_|GOLDEN_|STONE_|WOODEN_|LEATHER_|BOW|CROSSBOW|FISHING_ROD|SHEARS|SHIELD|TRIDENT|TURTLE_HELMET|ELYTRA|FLINT_AND_STEEL)"
  deny:
    - type: message
      messages:
        - "&cYou doesn't have an item in your hand."
```

In the example below, there is a check for the item in the player's hand. If the item matches the regex pattern, the player can open the inventory. Otherwise, they will receive a message, and the inventory will not open.

### Click Requirement

Defines multiple requirements for clicking the button. You need to specify several requirements and the corresponding clicks.

You can apply all clicks directly by using the following format:

```yaml
clicks:
  - ALL # or ANY
```

You can set the click type to `ALL` or `ANY` to apply the actions to all clicks. The list of clicks that will be included can be managed in the `config.json` file.

#### Example:

```yaml
click-requirement:
  left-click: # You must put a name for your requirement, it will not be used.
    clicks:
      - LEFT
      - SHIFT_LEFT
    requirements:
      - type: placeholder
        placeholder: "%player_gamemode%"
        value: "CREATIVE"
        action: equals_string
    deny:
      - type: sound
        sound: VILLAGER_NO
        pitch: 0.5f
        volume: 1.5f
    success:
      - type: message
        messages:
          - "&aLeft click !"
  right-click: # You must put a name for your requirement, it will not be used.
    clicks:
      - RIGHT
      - SHIFT_RIGHT
    requirements:
      - type: placeholder
        placeholder: "%player_gamemode%"
        value: "CREATIVE"
        action: equals_string
    deny:
      - type: sound
        sound: VILLAGER_NO
        pitch: 1.5f
        volume: 0.5f
    success:
      - type: message
        messages:
          - "&aRight click !"
```

## Requirements type

### `permission`

```yaml
- type: permission
  permission: <permission>
```

Checks if the player has the specified permission. To reverse the condition, add an exclamation mark `!` in front of the permission, like this: `!<permission>`.

### `placeholder`

```yaml
- type: placeholder
  placeholder: <placeholder>
  value: <placeholder value>
  action: <placeholder action>
  target: <player / placeholder with player name>
```

Allows you to define a permission using a placeholder. You must specify the placeholder, the action to be performed with the value, and the value that will be checked. For more information, [click here](https://docs.zmenu.dev/configurations/buttons#placeholder).

You can specify a player; otherwise, the player who opens the inventory will be used by default.

### `regex`

```yaml
- type: regex
  regex: <regex>
  input: <placeholder>
```

Checks if the input matches the specified regex pattern. The input can be a placeholder.

Visit [regexr.com](https://regexr.com) to create your regex pattern.

### `item`

```yaml
- type: item
  material: <material>
  amount: <amount of item>
  modelId: <model id> # default 0
```

Checks if the player has a specific item in their inventory.

### `job`

```yaml
- type: job
  job: <job name>
```

Allows to check if the player has the job. Works with [JobReborn](https://www.spigotmc.org/resources/jobs-reborn.4216/) plugin.

### `luckperm`

```yaml
- type: luckperm
  group: <group name>
```

Allows to check if the player is in a group. Works with [LuckPerms](https://www.spigotmc.org/resources/luckperms.28140/) plugin.

### `playername`

```yaml
- type: playername
  player-name: <placeholder>
```

Allows to check if a placeholder returns a text that can be a player nickname.

### `money`

```yaml
- type: money
  amount: <amount>
  currency: <currency name>
  economy: <economy name> # Only the zEssentials, CoinsEngine and EcoBits plugins need this
```

Check if the player has enough money in their account. This only works with [BeastTokens](https://www.spigotmc.org/resources/beasttokens-custom-currency.20806/), [Vault](https://www.spigotmc.org/resources/34315/), [PlayerPoints](https://www.spigotmc.org/resources/80745/), [ElementalTokens](https://builtbybit.com/resources/16707/), [ElementalGems](https://builtbybit.com/resources/14920/), [Level](https://www.minecraft.net/), [Experience](https://www.minecraft.net/), [**zEssentials**](https://www.spigotmc.org/resources/118014/), [EcoBits](https://www.spigotmc.org/resources/109967/), [CoinsEngine](https://www.spigotmc.org/resources/84121/) and [VotingPlugin](https://www.spigotmc.org/resources/15358/).\
CurrenciesAPI : [https://github.com/Traqueur-dev/CurrenciesAPI](https://github.com/Traqueur-dev/CurrenciesAPI)
