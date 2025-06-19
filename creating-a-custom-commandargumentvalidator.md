---
icon: message-check
---

# Creating a Custom CommandArgumentValidator

zMenu allows you to create custom command argument validators to check and transform arguments passed to your commands. This enables better control, type safety, and more helpful feedback.

In this guide, you'll learn how to create your own validator by following the example of the built-in `BooleanArgumentValidator`.

***

## Step 1: Implement the Interface

Create a class that implements `CommandArgumentValidator`.

Example: `BooleanArgumentValidator`

```java
package fr.maxlego08.menu.command.validators;

import fr.maxlego08.menu.api.command.CommandArgumentValidator;
import fr.maxlego08.menu.api.utils.Message;

public class BooleanArgumentValidator implements CommandArgumentValidator {
    @Override
    public boolean isValid(String value) {
        return value.equalsIgnoreCase("true") || value.equalsIgnoreCase("false");
    }

    @Override
    public Message getErrorMessage() {
        return Message.COMMAND_ARGUMENT_BOOLEAN;
    }

    @Override
    public String getType() {
        return "boolean";
    }
}
```

***

## Step 2: Register the Validator

You can register your validator using the zMenu command manager:

```java
commandManager.registerArgumentValidator(new BooleanArgumentValidator());
```

Once registered, it can be used in any command you define using zMenu’s command API.

***

## Step 3: Use in Command Definition

```yaml
commands:
  example:
    command: example
    inventory: example_with_boolean
    arguments:
      - name: active
        type: boolean
```

If the player runs `/example true`, it will resolve `true` into a `Boolean`.
