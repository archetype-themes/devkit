# Development workflow

Our component-first approach requires the [Shopify CLI plugin](https://github.com/archetype-themes/plugin-devkit) to be installed.

All plugin commands are [listed below](https://github.com/archetype-themes/plugin-theme-component?tab=readme-ov-file#list-of-commands) and you can learn more about [developing themes with components](https://github.com/archetype-themes/devkit/tree/main/1.%20Getting%20Started/Developing%20themes%20with%20components). In simple terms though, the development workflow is typically done in 3 different stages all using the plugin's commands:

## Creating components

You can create a new component with the `shopify theme component generate` command. This will generate a new theme component in the `components` directory with boilerplate code.

## Developing components

When developing a theme component, you have two separate workflows to choose from. You can either develop theme components:

- **Inside the [component explorer](https://github.com/archetype-themes/devkit/blob/main/2.%20Architecture/The%20Component%20Explorer.md)**: the `shopify theme component dev` command launches the component explorer and allows you to develop components in isolation.
- **Inside a [Shopify theme](https://github.com/archetype-themes/reference-theme)**: the `shopify theme component dev --theme-path="../reference-theme"` command allows you to develop your components within the context of a specified theme.

## Installing components

You can install a component (or list of components) with the `shopify theme component install` command. This command is only ran within a [Shopify theme](https://github.com/archetype-themes/reference-theme.git), which then imports the latest changes of your components directly into your theme.
