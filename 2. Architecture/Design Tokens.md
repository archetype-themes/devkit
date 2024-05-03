# Design tokens

Design tokens are the visual design atoms of theme components; they are used to maintain a scalable and consistent visual system for your UI/UX design. By defining attributes such as colors, font sizes, spacing, and more, design tokens facilitate consistency across different parts of your theme.

They help in maintaining visual consistency. They are stored as values (e.g., HEX codes for colors, numerical values for spacing) that can be applied universally across your theme components.

They are usually, but not always, tied to a global theme setting.

## CSS custom properties

This approach enables a centralized management of styling properties, creating a single source of truth. Changes to these properties automatically propagate throughout all theme components, ensuring that updates do not require manual updates across multiple files.

### The `css-variables` component

To manage these design tokens effectively, we included the [`css-variables`](https://github.com/archetype-themes/reference-components/blob/main/components/css-variables/css-variables.liquid) component. This component contains all our design tokens, including those for sizes, fonts, page layouts, border radii, and color schemes.

> [!NOTE] Although our current implementation is minimal, the goal is to expand this component into a comprehensive design token system applicable across all themes.

This `css-variables` file is included in the theme’s layout file using the following Liquid tag:

```liquid
{% render 'css-variables' %}
```

### Benefits of using design tokens

1. **Consistency**: Design tokens ensure that design decisions are applied consistently, regardless of who is implementing the feature or when it is being implemented.
2. **Maintainability**: With tokens, making changes to your design system (like altering the primary color or adjusting the spacing scale) becomes easier and universally applicable.
3. **Scalability**: As projects grow, tokens provide a scalable solution to manage design systems across large themes and an infinite number of theme components.

## Future direction

Moving forward, we plan to continuously refine our `css-variables` component, adding more tokens and enhancing its integration capabilities. This will allow developers and designers to adapt more easily to changing design needs and ensure that our theme components and our themes remain current.
