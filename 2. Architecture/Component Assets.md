# Component assets

The [Theme component plugin](https://github.com/archetype-themes/plugin-theme-component) compiles assets depending on their file type.

Asset files (CSS, JavaScript, SVG, etc.) added to your components will automatically be compiled to your Shopify theme's `assets/` directory.

## CSS

Any asset with the `.css` file extension is automatically transformed with [PostCSS](https://postcss.org/). Because we're catering to the modern web, the list of PostCSS plugins is intentionally lean:

- [PostCSS Preset Env](https://github.com/csstools/postcss-plugins/tree/main/plugin-packs/postcss-preset-env#readme): converts modern CSS into something most browsers can understand. We target the same list of browsers as Shopify by using their [browserlist-config](https://github.com/Shopify/web-configs/blob/main/packages/browserslist-config/README.md).
- [PostCSS Import](https://github.com/postcss/postcss-import/tree/master): resolves `@import` statements in CSS files.

For more information and to better understand how a theme component's CSS works, view the [Component CSS](https://github.com/archetype-themes/devkit/blob/main/2.%20Architecture/Component%20CSS.md) documentation.

## JavaScript

Unlike other types of assets, JavaScript files are not transformed in any way. They are preserved as is.

Any asset with the `.js` file extension is added to the list of modules to be resolved. This module list is based on the configuration in the component repository's [`import-map.json`](https://github.com/archetype-themes/reference-components/blob/main/importmap.json) file and this file can be updated depending on how you prefer to structure your JS files.

The list of modules is then injected as an import map in the form of a `import-map` snippet that should be included in your theme's layout file:

```liquid
{% render 'import-map' %}
```

For more information and to better understand how a theme component's JS works, view the [Import maps](https://github.com/archetype-themes/devkit/blob/main/2.%20Architecture/Import%20Maps.md) documentation.

## SVG

Any asset with the `.svg` file extension is automatically optimized with [SVGO](https://github.com/svg/svgo).
