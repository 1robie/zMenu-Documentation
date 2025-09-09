# Creating a Simple Dialog

This guide will walk you through creating your first dialog step by step.

## Step 1: Create the Dialog File

Create a new file in your `dialogs/` folder with a `.yml` extension:

```
plugins/zMenu/dialogs/welcome-dialog.yml
```

## Step 2: Basic Configuration

Start with the essential dialog properties:

```yaml
name: "&6&lWelcome Dialog"
external_title: "Welcome to our server!"
type: notice
```

### Required Fields

- **`name`** - The internal name of the dialog (supports color codes)
- **`external_title`** - The title shown in the dialog window
- **`type`** - The dialog type (`notice`, `confirmation`, `multi_action`, `server_links`)

## Step 3: Behavior Settings

Configure how the dialog behaves:

```yaml
can-close-with-escape: true
pause: false
after_action: CLOSE
```

### Behavior Options

- **`can-close-with-escape`** - Allow players to close with ESC key
- **`pause`** - Pause the game while dialog is open
- **`after_action`** - What happens after interaction: `CLOSE`, `PAUSE`, or `NONE`

## Step 4: Add Content

The `body` section contains what players see:

```yaml
body:
  welcome_message:
    type: plain_message
    messages:
      - "&6&lWelcome to our server!"
      - ""
      - "&7Thanks for joining us, &f%player_name%&7!"
      - "&7Current players online: &f%server_online%"
      - ""
      - "&eEnjoy your stay!"
    width: 400
```

## Step 5: Configure the Action Button

For a notice dialog, add the button configuration:

```yaml
notice:
  text: "&a&lI Understand"
  tooltip: "&7Click to continue"
  width: 200
```

## Complete Simple Dialog Example

Here's a complete working dialog:

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
      - "&6&lWelcome to our server!"
      - ""
      - "&7Thanks for joining us, &f%player_name%&7!"
      - "&7Current players online: &f%server_online%"
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
          - "&aWelcome message acknowledged!"
```

## Step 6: Test Your Dialog

To test your dialog, you can:

1. Use the dialog command: `/zmenu dialogs open welcome-dialog`
2. Trigger it through an action

## Tips for Simple Dialogs

- **Keep messages concise** - Players don't like to read walls of text
- **Use placeholders** - Make content dynamic with player/server data
- **Choose appropriate widths** - 300-500 pixels work well for most content
- **Add visual breaks** - Use empty lines (`""`) to separate content sections
- **Test on different screen sizes** - Ensure your dialog looks good everywhere

## Next Steps

Once you're comfortable with simple dialogs, explore:
- Different dialog types for various use cases
- Adding interactive inputs for data collection
- Using items and advanced body elements
- Creating complex multi-action dialogs