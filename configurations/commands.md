---
icon: square-terminal
---

# Commands

## Informations

The plugin has an `commands` folder that will contain all your commands. You can create an infinite number of commands. A command will contain the name of the command, its aliases, its permission and the name of the inventory to open.\
You can put several commands per file and create an unlimited number of files.

```
|- commands
  |- punish
    - punish.yml
  |- example
    - example.yml    
  - commands.yml
```

## Syntax

```yaml
commands:
  basic_command:
    command: basic_command
    inventory: basic_inventory
  advanced_command:
    command: advanced_command
    permission: "admin.use"
    deny-message: "§cYou don't have permission to use this command."
    aliases:
      - zai
    inventory: advanced_inventory
  pro_command:
    command: pro_command
    inventory: pro_inventory
  openbook:
    command: openbook
    actions:
      - type: book
        author: "Maxlego08" # Book author
        title: "&cTest" # Book title
        lines: # Book pages
          1: # First page
            - '     #34ebe8zMenu'
            - ''
            - ''
            - '<hover:show_text:"#34eba8Open an url !"><click:open_url:"https://minecraft-inventory-builder.com/">#f0af24Open URL<reset>'
  punish:
    command: punish
    permission: "admin.punish"
    aliases:
      - sanction
    inventory: example_punish
    arguments:
      - name: target
        type: online-player
      - name: reason
        auto-completion:
          - cheat
          - chat
          - skin
          - other
        actions:
          - type: message
            messages:
              - "&7You will put a punishment to the player &f&n%target%&r &7with the reason&8: &f%reason%"            
```

***

### `command`

```yaml
command: <command>
```

Main command

***

### `aliases`

```yaml
aliases:
  - <aliase 1>
  - <aliase 2>
  - ...
```

The aliases of the command.

***

### `actions`

```yaml
actions:
  - ...  
```

You can use [actions](actions.md) that will always be performed when executing the order.

***

### `permission`

```yaml
permission: <permission>
```

The permission the player must have to open the inventory.

***

### `inventory`

```yaml
inventory: <inventory name>
```

Name of the inventory that will be opened.

You can also specify the name of the plugin this way:

```yaml
inventory: "<plugin name>:<inventory name>"
```

***

### `arguments`

```yaml
arguments:
  - <arg1>
  - <arg2>
  - ...
```

Allows you to add arguments to your commands. You can use the arguments with the following placeholder: `%zmenu_argument_<argument name>%`&#x20;

### `deny-message`

```yaml
deny-message: "<message>"
```

Message sent to the player if he does not have permission to execute the command.

#### Example

```yaml
commands:
  punish:
    command: punish
    permission: "admin.punish"
    aliases:
      - sanction
    inventory: example_punish
    arguments:
      - name: target
        type: online-player
      - name: reason
        auto-completion:
          - cheat
          - chat
          - skin
          - other
        actions:
          - type: message
            messages:
              - "&7You will put a punishment to the player &f&n%target%&r &7with the reason&8: &f%reason%"
```

You can define an [action](actions.md), argument type and `auto-completion` list for each argument.

You can define whether an argument and required or not with the value `isRequired`, I’ll show you that in the example below.

You can not execute the actions of the main command with the value `performMainAction`

Here you have the command **`/punish <target> <reason`**> . So you can run the command this way: `/punish Maxlego08 Cheat (fly)`.

With the placeholders you will be able to retrieve the arguments:

| Placeholder               | Result        |
| ------------------------- | ------------- |
| `%zmenu_argument_target%` | `Maxlego08`   |
| `%zmenu_argument_reason%` | `Cheat (fly)` |

You can define whether the argument is optional and whether the argument has a specific inventory.

#### Example with no required argument:

```yaml
commands:
  warp:
    command: warp
    aliases:
      - warps
    inventory: warp
    arguments:
      - name: warp
        isRequired: false # Set the argument as optional
        performMainAction: false # Does not open inventory
        auto-completion:
          - minapvp
          - cajas
          - dungeon
          - encantamientos
          - jugadores
          - mercado
          - minas
          - rankup
        actions:
          - type: player_command
            commands:
              - "essentials:warp %zmenu_argument_warp% %player%"
```

This example opens a warp inventory, then with an argument to teleport the player to the desired warp using an aliase of essentials.

#### Argument validator

Allows you to verify that an argument is of the correct type

| Type          | Description                                                           |
| ------------- | --------------------------------------------------------------------- |
| boolean       | Checks if the argument is true or false                               |
| double        | Checks if the argument is a decimal number                            |
| entity-type   | Checks if the argument is an entity type                              |
| integer       | Checks if the argument is an number                                   |
| location      | Checks if the argument is a location (format: \<world>,\<x>,\<y>,\<z> |
| material      | Checks if the argument is a material                                  |
| online-player | Checks if the argument is an online player                            |
| player        | Checks if the argument is a player                                    |
| world         | Checks if the argument is a world name                                |

In this example, the target argument must be an online player.

```yaml
arguments:
  - name: target
    type: online-player
```
