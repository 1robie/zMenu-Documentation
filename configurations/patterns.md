# 🔋 Patterns

## Inventory

**Patterns** allow you to create reusable button configurations that can be applied across multiple inventories. This approach helps manage the decoration of your inventories efficiently, avoiding the need to replicate the same configurations multiple times.

#### How to Use Patterns

1. **Create Patterns**: Place your pattern files in the `patterns` folder. You can create as many patterns as you need to manage different decorative elements or layouts.
2. **Define Patterns**: Each pattern file will define a set of buttons and their configurations. Use these patterns to standardize and streamline the design of your inventories.
3. **Apply Patterns**: In your inventory configuration files, you can reference these patterns to apply them. This allows you to maintain consistency and easily update or modify the design elements across multiple inventories.

#### Example

For instance, if you have a pattern for a pagination button or a decorative border, you can define it in a pattern file and then include that pattern in various inventory configurations. This way, any changes to the pattern will automatically reflect in all inventories that use it.

#### Benefits

* **Efficiency**: Avoid duplicating button configurations.
* **Consistency**: Maintain a uniform look across different inventories.
* **Ease of Management**: Update design elements in one place and see the changes applied everywhere.

By leveraging patterns, you can effectively manage and customize the appearance of your inventories without redundant configuration efforts.

[Example](../plugins-files.md#pattern1):

```yaml
name: "pattern1"
size: 54
# Displays the pattern on multiple pages, false by default
enableMultiPage: <true/false>
items:
    ...
```

A pattern must contain a `name`, its name will be used in inventories to identify the pattern.&#x20;

You then have a `size`, which is that of the inventory, you have to put patterns of the same size with the inventories, a pattern of size 18 cannot go with an inventory of cut 27 for example.

You then have a list of items, it’s the same as for [inventories](inventories.md#items).

## Button

You can create a pattern for your buttons to avoid having to repeat the same thing hundreds of times. You will save hours of configuration with this system.

### How to create a pattern ?

You must create a yml file in the pattern folder, the file name is important. It will be used in your inventory file. In the file you must specify the name, type and button. A default file will look like this:

```yaml
name: "<your name>"
type: BUTTON
button:
```

You can then configure your button as you do for inventories. Except that here you will be able to define variables from the inventory file that will be used here. You can define an infinite number of variables, it all depends on your need.

Here is an example of a pattern with the name and slot that will change.

```yaml
name: 'Example'
type: BUTTON
button:
  slot: '%slot%'
  item:
    material: PAPER
    name: "&c%name%"
```

A variable can have prefixes to change their uses.

<table data-full-width="true"><thead><tr><th>Prefix</th><th>Definition</th></tr></thead><tbody><tr><td><code>%upper_&#x3C;key>%</code></td><td>Displays the text in uppercase</td></tr><tr><td><code>%lower_&#x3C;key>%</code></td><td>Displays the text in lowercase</td></tr><tr><td><code>%capitalize_&#x3C;key>%</code></td><td>Display the text in capital</td></tr><tr><td><code>%add_one_&#x3C;key>%</code></td><td>Allows to add one to the value, attention the value must be a number.</td></tr><tr><td><code>%remove_one_&#x3C;key>%</code></td><td>Allows to remove one has the value, attention the value must be mandatory a number.</td></tr></tbody></table>

### How to use a pattern

Using a pattern is very simple. Simply display the pattern configuration in your button, set the file name and put your placeholders. For the example if above we will have:

```yaml
name: 'Example'
size: 54
items:
  example1:
    pattern:
      fileName: "<your file name>"
      slot: 10
      name: 'Example 1'
  example2:
    pattern:
      fileName: "<your file name>"
      slot: 12
      name: 'Example 1'
```

The pattern can be used endlessly in inventory. This allows to create very optimized configs without having to repeat the same thing several times. Only the important items will be in your inventory file.

### Example

This example provient de la resource [Vote Menu](https://builtbybit.com/resources/vote-menu-zmenu-configurations.41468/).

#### Inventory Shop

```yaml
name: '&l#8fa3e8ᴠᴏᴛᴇ sʜᴏᴘ'
size: 54
items:

  shop1:
    pattern:
      fileName: "vote_shop" # 
      slot: 20
      point: 10
      material: DIAMOND_BLOCK
      name: ' #3f3f3f▷ #6ff8edDiamond Blocks #3f3f3f◁'
      description:
        - '#3f3f3f• &fx16 Diamond Blocks'
      commands:
        - 'give %player% diamond_block 16'

  shop2:
    pattern:
      fileName: "vote_shop"
      slot: 21
      point: 20
      material: EMERALD_BLOCK
      name: ' #3f3f3f▷ #40f082Emerald Blocks #3f3f3f◁'
      description:
        - '#3f3f3f• &fx16 Emerald Blocks'
      commands:
        - 'give %player% emerald_block 16'

  shop3:
    pattern:
      fileName: "vote_shop"
      slot: 22
      point: 6
      material: IRON_BLOCK
      name: ' #3f3f3f▷ #e3e3e3Iron Blocks #3f3f3f◁'
      description:
        - '#3f3f3f• &fx16 Iron Blocks'
      commands:
        - 'give %player% iron_block 16'
```

#### Pattern

```yaml
name: 'Vote Reward'
type: BUTTON
button:
  slot: '%slot%'
  view_requirement:
    requirements:
      - type: placeholder
        placeholder: "%zmenu_player_value_vote_points%"
        value: '%point%'
        action: LOWER
  updateOnClick: true
  actions:
    - type: sound
      sound: ENTITY_VILLAGER_NO
  item:
    material: '%material%'
    name: '%name%'
    lore:
      - ''
      - '#ffd353⛃ ᴅᴇsᴄʀɪᴘᴛɪᴏɴ#3f3f3f:'
      - '%description%'
      - ''
      - '#ffd353🌟 ᴘʀɪᴄᴇ#3f3f3f: #8fa3e8%point% points'
      - ''
      - '#ff0000✘ ʏᴏᴜ ᴅᴏɴ’ᴛ ʜᴀᴠᴇ ᴇɴᴏᴜɢʜ ᴠᴏᴛᴇ ᴘᴏɪɴᴛs'
  else:

    updateOnClick: true
    refreshOnClick: true
    click_requirement:
      right_click:
        clicks:
          - ALL
        requirements:
          - type: placeholder
            placeholder: "%zmenu_player_value_vote_points%"
            value: '%point%'
            action: SUPERIOR_OR_EQUAL
        deny:
          - type: sound
            sound: VILLAGER_NO
          - type: message
            messages:
              - "#3f3f3f[#ff0000✘#3f3f3f] #ff0000An error has occurred, please re-open the inventory."
          - type: close
        success:
          - type: data
            action: SUBTRACT
            key: 'vote_points'
            value: '%point%'
          - type: console_command
            commands:
              - '%commands%'
          - type: sound
            sound: ENTITY_PLAYER_LEVELUP

    item:
      material: '%material%'
      name: '%name%'
      lore:
        - ''
        - '#ffd353⛃ ᴅᴇsᴄʀɪᴘᴛɪᴏɴ#3f3f3f:'
        - '%description%'
        - ''
        - '#ffd353🌟 ᴘʀɪᴄᴇ#3f3f3f: #8fa3e8%point% points'
        - ''
        - '#ffd353➥ ᴄʟɪᴄᴋ ᴛᴏ ᴘᴜʀᴄʜᴀsᴇ'
```
