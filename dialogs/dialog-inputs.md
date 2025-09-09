# Dialog Inputs

Dialog inputs allow you to collect information from players through interactive form elements. All input values can be accessed in actions using placeholders.

## Available Input Types

### Text Input (`dialog_text`)

Collect text input from players with single or multi-line support.

```yaml
inputs:
  player_feedback:
    type: dialog_text
    label: "&6Share your thoughts about our server:"
    width: 400
    label-visible: true
    initial-value: "This server is amazing because..."
    max-length: 200
    multiline:
      max-lines: 4
      height: 80
```

**Options:**
- `label` - Text shown above the input field
- `width` - Input field width in pixels
- `label-visible` - Whether to show the label
- `initial-value` - Pre-filled text
- `max-length` - Maximum character limit
- `multiline` - Multi-line text area configuration
    - `max-lines` - Maximum number of lines
    - `height` - Height in pixels

**Accessing value:** `%player_feedback%`

### Boolean Input (`dialog_boolean`)

Present a true/false choice to players.

```yaml
inputs:
  newsletter:
    type: dialog_boolean
    label: "&eWould you like to receive server updates?"
    initial-value: true
    text-true: "&a&lYES, keep me updated!"
    text-false: "&c&lNo, thanks."
```

**Options:**
- `label` - Question or prompt text
- `initial-value` - Default selection (true/false)
- `text-true` - Text for the "true" option
- `text-false` - Text for the "false" option

**Accessing value:** `%newsletter%` (returns "true" or "false")

### Single Option Selection (`dialog_single_option`)

Allow players to choose one option from multiple choices.

```yaml
inputs:
  gamemode:
    type: dialog_single_option
    label: "&6What's your favorite game mode?"
    label-visible: true
    options:
      option1:
        id: "survival"
        display: "&2🌱 Survival Mode"
        initial: true
      option2:
        id: "creative"
        display: "&6🎨 Creative Mode"
        initial: false
      option3:
        id: "adventure"
        display: "&5⚔️ Adventure Mode"
        initial: false
      option4:
        id: "pvp"
        display: "&c⚡ PvP Arena"
        initial: false
```

**Options:**
- `label` - Question or prompt text
- `label-visible` - Whether to show the label
- `options` - Available choices
    - `id` - Unique identifier for the option
    - `display` - Text shown to the player
    - `initial` - Whether this option is selected by default

**Accessing value:** `%gamemode%` (returns the selected option's `id`)

### Number Range (`dialog_number_range`)

Let players select a number within a specified range.

```yaml
inputs:
  playtime:
    type: dialog_number_range
    label: "&eHow many hours do you play per day?"
    label-format: "options.generic_value"
    width: 350
    start: 1
    end: 12
    step: 1
    initial-value: 3
```

**Options:**
- `label` - Question or prompt text
- `label-format` - Display format for the current value
- `width` - Slider width in pixels
- `start` - Minimum value
- `end` - Maximum value
- `step` - Increment/decrement step
- `initial-value` - Default selected value

**Accessing value:** `%playtime%` (returns the selected number)

## Using Input Values in Actions

All input values are automatically available as placeholders in your dialog actions:

```yaml
actions:
  1:
    success:
      - type: message
        messages:
          - "&aThank you for your feedback!"
          - "&7Text: &f%player_feedback%"
          - "&7Newsletter: &f%newsletter%"
          - "&7Favorite mode: &f%gamemode%"
          - "&7Daily playtime: &f%playtime% hours"
```

### Conditional Content

You can use requirements and placeholders to show different content based on conditions:

```yaml
inputs:
  vip_feedback:
    type: dialog_text
    label: "&6VIP Members: Share your exclusive feedback!"
    width: 400
    label-visible: true
    initial-value: "As a VIP, I think..."
    max-length: 200
    multiline:
      max-lines: 4
      height: 80
    view-requirements:
      - type: permission
        permission: "zmenu.vip"
    else:
      type: dialog_text
      label: "&7Share your feedback (non-VIP):"
      width: 400
      label-visible: true
      initial-value: "I think..."
      max-length: 200
      multiline:
        max-lines: 4
        height: 80
```

## Input Validation

### Text Input Validation
- Automatic length validation based on `max-length`
- Empty input handling
- Special character support

### Boolean Input Validation
- Always returns valid true/false values
- No additional validation needed

### Single Option Validation
- Ensures one option is always selected
- Returns the `id` of the selected option

### Number Range Validation
- Automatic range validation (stays within start/end bounds)
- Step validation ensures valid increments

## Best Practices

1. **Use clear labels** - Make it obvious what you're asking for
2. **Set reasonable limits** - Don't overwhelm players with too many options
3. **Provide good defaults** - Use sensible initial values
4. **Keep it relevant** - Only ask for information you'll actually use
5. **Test thoroughly** - Ensure all input combinations work correctly

## Styling Tips

- **Consistent widths** - Use similar widths for related inputs
- **Appropriate sizing** - Don't make inputs too small or too large
- **Visual grouping** - Group related inputs together
- **Color coding** - Use colors to indicate input importance or type