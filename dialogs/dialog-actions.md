# Dialog Actions

Dialog actions in zMenu use the same action system as menus, but with some limitations. Not all menu actions are available in dialogs due to the different context and user experience considerations.

## Action Compatibility

**Important:** Dialogs support most of the same actions as regular zMenu buttons, but some actions are not available or behave differently in the dialog context.

For a complete and up-to-date list of which actions are supported in dialogs, please refer to the **Actions** section in the Configurations documentation, where you'll find a comprehensive table indicating action availability for both menus and dialogs.

## Action Structure

Dialog actions follow the same structure as menu actions:

```yaml
actions:
  1:
    requirements:  # Optional conditions
      - type: placeholder
        placeholder: "%player_gamemode%"
        value: "SURVIVAL"
        action: EQUALS
    success:       # Actions to execute on success
      - type: message
        messages:
          - "&aAction executed successfully!"
    deny:          # Actions to execute if requirements fail
      - type: message
        messages:
          - "&cRequirements not met!"
```

## Context-Specific Considerations

### Dialog-Specific Variables

Dialogs have access to special placeholder variables from input fields:

- `%input_name%` - Value from text inputs
- `%boolean_name%` - Value from boolean inputs (true/false)
- `%boolean_name_text%` - Value defined for true/false states in boolean inputs
- `%single_option_name%` - Selected option ID from single option inputs
- `%number_range_name%` - Selected number from range inputs

### Action Timing

Dialog actions execute when:

- **Notice dialogs:** When the OK button is clicked
- **Confirmation dialogs:** When Yes or No is clicked (separate action sets)
- **Multi-action dialogs:** When any custom button is clicked
- **Server links dialogs:** When the main action button is clicked

## Action Limitations in Dialogs

Some actions that work in regular menus may not be available or may behave differently in dialogs. Always check the action compatibility table in the main Actions documentation to ensure the actions you want to use are supported in the dialog context.

---