#### CSS styles

Each component can have its own `main.css` file, which will encapsulate the specific CSS styles of that component. Below are the guidelines on how CSS is managed in our own components:

- **Component-specific CSS**: The unique CSS styles for each component should be contained within its `main.css` file.
- **Importing shared CSS**: Shared CSS files can be imported into `main.css` by referencing the paths to these files, typically located in the repository's root `styles/` folder.
- **Leveraging CSS variables**: Components may use custom CSS variables defined anywhere within the theme's CSS. Typically, these components leverage the variables specified in the [`css-variables.liquid`](https://github.com/archetype-themes/reference-components/blob/937dfb7dbc57062f9fc8c23bcb59189088c5304c/components/css-variables/css-variables.liquid) component.
- **Modern CSS and compatibility**: Modern CSS syntax is encouraged and supported. CSS files are processed using [PostCSS](https://postcss.org/) to ensure compatibility across various browsers, enabling the use of the latest CSS features.
- **Overriding component CSS**: CSS from any component can be overridden by including a specific CSS file within the theme that targets and overrides the predefined styles.

These guidelines help maintain a consistent and manageable approach to CSS across all components, supporting straightforward customization and updates.