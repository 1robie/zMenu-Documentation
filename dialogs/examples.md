# Dialog Examples

Here are complete, working examples of different dialog types that you can use as templates for your own dialogs.

## Example 1: Simple Notice Dialog

A basic welcome dialog for new players.

```yaml
name: "&6&lWelcome Dialog"
external_title: "Welcome to our server!"
type: notice

can-close-with-escape: true
pause: false
after_action: CLOSE

body:
  welcome_message:
    type: plain_message
    messages:
      - "&6&lWelcome to our amazing server!"
      - ""
      - "&7Server Name: &f%server_name%"
      - "&7Your Name: &f%player_name%"
      - "&7Players Online: &f%server_online%"
      - ""
      - "&eEnjoy your stay and have fun!"
    width: 400

notice:
  text: "&a&lI Understand"
  tooltip: "&7Click to continue"
  width: 200

actions:
  1:
    success:
      - type: message
        messages:
          - "&aWelcome to the server!"
```

## Example 2: Confirmation Dialog with Inputs

A feedback collection dialog with confirmation.

```yaml
name: "&6&lServer Feedback Dialog"
external_title: "Share Your Feedback"
type: confirmation

can-close-with-escape: true
pause: false
after_action: CLOSE

body:
  feedback_intro:
    type: plain_message
    messages:
      - "&6&lWe'd love your feedback!"
      - ""
      - "&7Your opinion helps us improve"
      - "&7the server experience for everyone."
      - ""
      - "&ePlease take a moment to share your thoughts:"
    width: 450

inputs:
  feedback_text:
    type: dialog_text
    label: "&6What do you think about our server?"
    width: 400
    label-visible: true
    initial-value: "I really enjoy..."
    max-length: 300
    multiline:
      max-lines: 5
      height: 100
  
  recommend:
    type: dialog_boolean
    label: "&eWould you recommend us to friends?"
    initial-value: true
    text-true: "&a&lYES, definitely!"
    text-false: "&c&lNot really."
  
  rating:
    type: dialog_number_range
    label: "&6Rate our server (1-10):"
    width: 300
    start: 1
    end: 10
    step: 1
    initial-value: 8

confirmation:
  yes-text: "&a&lSubmit Feedback"
  yes-tooltip: "&7Click to send your feedback"
  yes-width: 200
  no-text: "&c&lCancel"
  no-tooltip: "&7Click to cancel"
  no-width: 150

yes-actions:
  1:
    success:
      - type: message
        messages:
          - "&aThank you for your feedback!"
          - "&7Rating: &f%rating%/10"
          - "&7Recommendation: &f%recommend%"
      - type: console_command
        commands:
          - "tell @a %player% just submitted feedback!"

no-actions:
  1:
    success:
      - type: message
        messages:
          - "&7Feedback cancelled. Thanks anyway!"
```

## Example 3: Multi-Action Server Navigation

A dialog for server navigation with multiple options.

```yaml
name: "&6&lServer Navigation"
external_title: "Where would you like to go?"
type: multi_action

can-close-with-escape: true
pause: false
after_action: CLOSE
number-of-columns: 2

body:
  navigation_info:
    type: plain_message
    messages:
      - "&6&lServer Navigation"
      - ""
      - "&7Choose your destination:"
    width: 400

multi-actions:
  survival:
    text: "&a&lSurvival World"
    tooltip: "&7Join the main survival world"
    width: 200
    actions:
      1:
        success:
          - type: player_command
            commands:
              - "warp survival"
          - type: message
            messages:
              - "&aWelcome to Survival World!"
  
  creative:
    text: "&b&lCreative World"
    tooltip: "&7Build anything you can imagine"
    width: 200
    actions:
      1:
        success:
          - type: player_command
            commands:
              - "warp creative"
          - type: message
            messages:
              - "&bWelcome to Creative World!"
  
  minigames:
    text: "&e&lMinigames"
    tooltip: "&7Play fun minigames with others"
    width: 200
    actions:
      1:
        success:
          - type: player_command
            commands:
              - "warp minigames"
          - type: message
            messages:
              - "&eWelcome to the Minigames Hub!"
  
  spawn:
    text: "&f&lReturn to Spawn"
    tooltip: "&7Go back to the main spawn area"
    width: 200
    actions:
      1:
        success:
          - type: player_command
            commands:
              - "spawn"
          - type: message
            messages:
              - "&fReturning to spawn..."
```

## Example 4: Enhanced Dialog with Items

A dialog showcasing items with rich content.

```yaml
name: "&6&lServer Features"
external_title: "Discover Our Features"
type: notice

can-close-with-escape: true
pause: false
after_action: CLOSE

body:
  intro:
    type: plain_message
    messages:
      - "&6&lDiscover Our Amazing Features!"
      - ""
      - "&7Our server offers unique gameplay experiences:"
    width: 450
  
  featured_item:
    type: item
    item:
      material: DIAMOND_SWORD
      name: "&b&lLegendary Server Sword"
      lore:
        - ""
        - "&7This represents our custom"
        - "&7item enhancement system."
        - ""
        - "&6Features:"
        - "&e✦ Custom Enchantments"
        - "&e✦ Unique Abilities"
        - "&e✦ Progressive Upgrades"
        - ""
        - "&c&lThis is just a preview!"
      enchantments:
        - SHARPNESS:10
        - UNBREAKING:5
      glowing: true
    
    description:
      messages:
        - "&7Our server features over 100"
        - "&7custom items with unique abilities."
        - ""
        - "&eExplore the world to find them all!"
      width: 350
    
    show-decoration: true
    show-tooltip: true
    width: 200
    height: 150

notice:
  text: "&a&lAwesome!"
  tooltip: "&7Click to start exploring"
  width: 180

actions:
  1:
    success:
      - type: message
        messages:
          - "&aHappy exploring, &f%player_name%&a!"
      - type: player_command
        commands:
          - "kit starter"
```

## Usage Tips

1. **Start simple** - Begin with basic notice dialogs before adding complexity
2. **Test incrementally** - Add one feature at a time and test
3. **Use meaningful names** - Choose clear file names and internal names
4. **Plan your flow** - Think about what happens after the dialog closes
5. **Consider your audience** - Design dialogs appropriate for your server's players

## Common Mistakes to Avoid

- **Missing required fields** - Always include name, external_title, and type
- **Incorrect indentation** - YAML is sensitive to proper spacing
- **Overly wide content** - Keep widths reasonable for different screen sizes
- **Too much text** - Break up long content into multiple sections
- **Forgetting actions** - Always provide feedback for player interactions