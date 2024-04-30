## Distinction between theme component files and theme files

Theme component files focus on presentation and user interaction, making them customizable and reusable across any number of themes while theme files maintain the functionality of the store by managing state and defining the settings to be included. The specific settings included as part of theme files directly influence the behavior of theme components.

The goal is to enforce a clear separation of concerns between theme component files and theme files.

### Theme component files

Theme component files primarily manage the visual presentation of the theme. These files are modular and are specifically designed to handle how elements look and behave on the front-end.

A theme component accepts inputs that adjust its behavior and/or appearance in the form of **parameters**. Parameters allow developers to pass specific values that tailor the component's functionality or style according to the needs of the theme, and typically, but not always, reference:

- **Theme editor settings**: Components use settings defined within the Shopify theme editor to adapt to different configurations and enables theme developers (and users) to customize components without directly editing code.
- **Liquid objects/values**: Component files can access and use global variables defined across the Shopify platform and/or values that are passed directly to them.

### Theme files

Theme files are responsible for managing and maintaining the state across the entire theme. They ensure that the theme is the one to store values for its settings and configurations so that theme components can then use these values. Theme files include:

- **Config files**: for example `config/settings_schema.json` and `config/settings_data.json` manage the global settings of the theme.
- **Layout files**: for example `layout/*.liquid` acts as a main entry point for themes where the global state is manually configured.
- **Section and template files**: for example `sections/*.liquid` and `template/*.json` files control the state at a more granular level, such as within individual sections or blocks by defining theme editor settings.