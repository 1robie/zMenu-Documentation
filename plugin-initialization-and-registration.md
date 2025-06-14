---
description: >-
  In this final section, you'll learn how everything comes together in the main
  plugin class.
icon: square-check
---

# Plugin Initialization and Registration

## Goal

Ensure that all components (loaders, actions, permissibles, inventories) are registered properly when the plugin is enabled.

### Step 1: Create Your Main Class

Example: `ZMenuExample.java`

```java
import fr.maxlego08.example.buttons.BooksButton;
import fr.maxlego08.example.loaders.BasicLoader;
import fr.maxlego08.example.loaders.ExampleActionLoader;
import fr.maxlego08.example.loaders.ExampleMaterialLoader;
import fr.maxlego08.example.loaders.ExamplePermissibleLoader;
import fr.maxlego08.menu.api.ButtonManager;
import fr.maxlego08.menu.api.InventoryManager;
import fr.maxlego08.menu.api.exceptions.InventoryException;
import fr.maxlego08.menu.api.loader.NoneLoader;
import fr.maxlego08.menu.api.pattern.PatternManager;
import org.bukkit.plugin.RegisteredServiceProvider;
import org.bukkit.plugin.java.JavaPlugin;

public final class ZMenuExample extends JavaPlugin {

    @Override
    public void onEnable() {

        this.saveDefaultConfig();

        InventoryManager inventoryManager = getProvider(InventoryManager.class);
        ButtonManager buttonManager = getProvider(ButtonManager.class);
        PatternManager patternManager = getProvider(PatternManager.class);

        // Register custom material loader
        inventoryManager.registerMaterialLoader(new ExampleMaterialLoader());

        // Register custom button loaders
        buttonManager.register(new BasicLoader(this));
        buttonManager.register(new NoneLoader(this, BooksButton.class, "PAGINATION_EXAMPLE"));

        // Register actions and permissions
        buttonManager.registerAction(new ExampleActionLoader());
        buttonManager.registerPermissible(new ExamplePermissibleLoader(buttonManager));

        // Load inventory file
        try {
            inventoryManager.loadInventoryOrSaveResource(this, "inventories/example.yml");
        } catch (InventoryException exception) {
            exception.printStackTrace();
        }
    }

    @Override
    public void onDisable() {
        // Any cleanup if needed
    }

    private <T> T getProvider(Class<T> classz) {
        RegisteredServiceProvider<T> provider = getServer().getServicesManager().getRegistration(classz);
        if (provider == null) {
            throw new RuntimeException("Unable to retrieve the provider " + classz);
        }
        return provider.getProvider();
    }
}
```

### Step 2: Define plugin.yml

```yaml
name: zMenuExample
version: '1.0.0'
main: fr.maxlego08.example.ZMenuExample
api-version: '1.21'
authors: [Maxlego08]
description: Example for zMenu
website: https://groupez.dev/
```

### Result

Once compiled and installed on your server with zMenu installed, your plugin will:

* Register all custom logic
* Load inventories
* Be ready to use `/menu open example` or call menus programmatically
