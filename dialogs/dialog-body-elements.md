# Dialog Body Elements

Dialog body elements are the building blocks of your dialog content. You can combine different element types to create rich, engaging dialogs that provide information and showcase features.

## Element Types Overview

The `body` section supports two main types of elements:

1. **Plain Message** - Text content with formatting and placeholders
2. **Item Display** - Minecraft items with descriptions and tooltips

## Plain Message Elements

Plain message elements display formatted text to players.

### Basic Configuration

```yaml
body:
  my_message:
    type: plain_message
    messages:
      - "&6&lTitle Text"
      - ""
      - "&7Regular content line"
      - "&eHighlighted information"
    width: 400
```

### Advanced Text Formatting

```yaml
body:
  formatted_content:
    type: plain_message
    messages:
      - "&a&l▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄"
      - "&6          SERVER INFORMATION"
      - "&a&l▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄"
      - ""
      - "&7Server Name: &f%server_name%"
      - "&7Current World: &f%player_world%"
      - "&7Your Level: &f%player_level%"
      - "&7Balance: &f$%player_money%"
      - ""
      - "&b▸ &7Players Online: &f%server_online%&7/&f%server_max%"
      - "&b▸ &7Server TPS: &f%server_tps%"
      - "&b▸ &7Current Time: &f%server_time%"
      - ""
      - "&eThank you for being part of our community!"
    width: 500
```

### Color Code Reference

Supported Minimessage and Minecraft color codes:

| Code | Color | Code | Format |
|------|-------|------|--------|
| `&0` | Black | `&l` | Bold |
| `&1` | Dark Blue | `&m` | Strikethrough |
| `&2` | Dark Green | `&n` | Underline |
| `&3` | Dark Aqua | `&o` | Italic |
| `&4` | Dark Red | `&r` | Reset |
| `&5` | Dark Purple | | |
| `&6` | Gold | | |
| `&7` | Gray | | |
| `&8` | Dark Gray | | |
| `&9` | Blue | | |
| `&a` | Green | | |
| `&b` | Aqua | | |
| `&c` | Red | | |
| `&d` | Light Purple | | |
| `&e` | Yellow | | |
| `&f` | White | | |



## Item Display Elements

Item elements show Minecraft items with optional descriptions.

### Basic Item Display

```yaml
body:
  showcase_item:
    type: item
    item:
      material: DIAMOND_SWORD
      name: "&b&lServer Sword"
      lore:
        - "&7A special weapon for our players"
      glowing: true
    
    width: 150
    height: 120
```

### Item Configuration Options

Same synthax as [items](../configurations/items.md) in inventory 

#### Display Settings
```yaml
show-decoration: true         # Show durability bar and stack count
show-tooltip: true           # Enable hover tooltips
width: 200                   # Display width (1-256)
height: 150                  # Display height (1-256)
```

### Conditional Content

You can use requirements and placeholders to show different content based on conditions:

```yaml
body:
  conditional_message:
    type: plain_message
    messages:
      - "&6&lVIP Welcome!"
      - "&7Welcome back, &f%player_name%&7!"
      - "&7Your VIP privileges are active."
    width: 350
    view-requirements:
      - type: permission
        permission: "zmenu.vip"
    else:
      messages:
        - "&7Welcome back, &f%player_name%&7!"
        - "&7Consider upgrading to VIP for extra benefits!"
      width: 350
```

## Combining Elements

### Effective Element Combinations

**Information + Visual:**
```yaml
body:
  intro:
    type: plain_message
    messages:
      - "&6&lServer Shop"
      - "&7Browse our available items:"
    width: 300
  
  featured_item:
    type: item
    # item configuration
    width: 150
  
  details:
    type: plain_message
    messages:
      - "&7Use &f/shop &7to access the full store"
    width: 300
```

**Story + Evidence:**
```yaml
body:
  story:
    type: plain_message
    messages:
      - "&6&lThe Legend of the Ancient Blade"
      - ""
      - "&7Long ago, a legendary weapon was"
      - "&7forged by the server's founders..."
    width: 450
  
  legendary_item:
    type: item
    # ancient blade configuration
    width: 200
  
  conclusion:
    type: plain_message
    messages:
      - "&7This blade now awaits a worthy hero."
      - "&eWill you be the chosen one?"
    width: 450

```