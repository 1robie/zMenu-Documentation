# Dialog Configuration Options

This page covers all the configuration options available for dialogs, including basic properties, behavior settings, and type-specific configurations.

## Basic Dialog Properties

### Required Properties

```yaml
name: "&6&lMy Dialog"           # Internal dialog name (supports color codes)
external_title: "Dialog Title"  # Title displayed in the dialog window
type: notice                    # Dialog type (see Dialog Types page)
```

- **`name`** - The internal identifier for the dialog. Supports Minecraft color codes and formatting.
- **`external_title`** - The title shown at the top of the dialog window. Plain text only.
- **`type`** - Determines the dialog behavior and available options.

## Behavior Settings

### General Behavior

```yaml
can-close-with-escape: true  # Allow ESC key to close dialog
pause: false                 # Pause the game while dialog is open
after_action: CLOSE         # Action after dialog interaction
```

- **`can-close-with-escape`** (boolean, default: true)
    - `true` - Players can press ESC to close the dialog
    - `false` - ESC key is disabled, players must use dialog buttons

- **`pause`** (boolean, default: false)
    - `true` - Game is paused while dialog is open
    - `false` - Game continues normally

- **`after_action`** (string, default: CLOSE)
    - `CLOSE` - Dialog closes after action execution
    - `PAUSE` - Dialog stays open after action
    - `NONE` - No specific behavior after action

## Type-Specific Configurations

### Notice Dialog Configuration

```yaml
type: notice
notice:
  text: "&a&lOK"              # Button text
  tooltip: "&7Click to close"  # Button tooltip
  width: 150                   # Button width in pixels
```

### Confirmation Dialog Configuration

```yaml
type: confirmation
confirmation:
  yes-text: "&a&lYes"         # Accept button text
  yes-tooltip: "&7Click to confirm"  # Accept button tooltip
  yes-width: 120              # Accept button width
  no-text: "&c&lNo"           # Decline button text
  no-tooltip: "&7Click to cancel"   # Decline button tooltip
  no-width: 120               # Decline button width
```

### Multi-Action Dialog Configuration

```yaml
type: multi_action
number-of-columns: 2         # Buttons per row (1-10)
multi-actions:
  button_id:
    text: "&e&lButton Text"
    tooltip: "&7Button description"
    width: 200
    actions:                 # Action configuration
      1:
        success:
          - type: message
            messages:
              - "&aButton clicked!"
```

**Multi-Action Options:**
- **`number-of-columns`** - How many buttons to display per row
- **`multi-actions`** - Collection of custom buttons
    - Each button needs: `text`, `tooltip`, `width`, and `actions`

### Server Links Dialog Configuration

```yaml
type: server_links
server-links:
  text: "&6&lServer Links"
  tooltip: "&7Click to open links"
  width: 300
  number-of-columns: 2
  actions:                   # Main action configuration
    1:
      success:
        - type: message
          messages:
            - "&aOpening server links..."
```

## Advanced Configuration

### Custom Styling

```yaml
# Example of advanced styling options
body:
  styled_message:
    type: plain_message
    messages:
      - "&a&l▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄"
      - "&6Server Information"
      - "&a&l▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄"
      - ""
      - "&7Content goes here..."
    width: 500
```

## Configuration Validation

### Common Validation Rules

1. **Width values** must be between specified ranges
2. **Dialog types** must be one of the supported types
3. **Action structure** must follow zMenu action format
4. **YAML syntax** must be valid (proper indentation and structure)

### Error Prevention

- Always validate your YAML syntax
- Test with minimal configurations first
- Check server logs for configuration errors
- Use consistent naming conventions
- Verify all referenced placeholders exist

## Performance Considerations

- **Limit concurrent dialogs** - Don't show multiple dialogs simultaneously
- **Optimize content size** - Large dialogs can impact performance
- **Minimize complex actions** - Keep dialog actions lightweight
- **Cache frequently used dialogs** - Reuse dialog configurations when possible

## Best Practices

1. **Keep it simple** - Start with basic configurations and add complexity gradually
2. **Test thoroughly** - Always test dialogs with different player scenarios
3. **Use consistent styling** - Maintain visual consistency across all dialogs
4. **Document your dialogs** - Comment complex configurations for future reference
5. **Plan user flow** - Consider what happens before and after the dialog