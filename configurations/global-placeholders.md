---
icon: earth-europe
---

# Global Placeholders

In the `global-placeholders.yml` file, you can define values that will be available across all inventory configuration files.\
This helps streamline your configurations by centralizing common placeholders.

## Global Placeholders

```yaml
example-a: "Hey im an example !"

example-b:
  - "Dont forgot"
  - "To purchase zEssentials"
```

You can define any value for the placeholders. If you define a list, the placeholder must be used within a list.

#### Example:

```yaml
item-in-second-page:
  type: INVENTORY
  slot: 22
  page: 2
  inventory: "basic_inventory"
  plugin: "zMenu"
  item:
    material: COMPASS
    name: "&fOpen basic inventory &8- &7%example-a%" # Use of global placeholder
    lore:
      - "&7Click here for open"
      - "&7the &fbasic inventory"
      - "%example-b%" # Use of global placeholder
```

## Modifications

### **Upper**

`%upper_<placeholder name>%` transforms your text to uppercase.

### **Lower**

`%lower_<placeholder name>%` transforms your text to lowercase.

### **Capitalize**

`%capitalize_<placeholder name>%` capitalizes your text (the first letter will be uppercase, and the rest lowercase).

### **Add One**

`%add_one_<placeholder name>%` adds 1 to your placeholder. This only works if the value is a number.

### **Remove One**

`%remove_one_<placeholder name>%` subtracts 1 from your placeholder. This only works if the value is a number.

