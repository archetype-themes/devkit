#### Import maps

We embrace the modern web, and we recognize the importance of a simpler and more straightforward approach to JavaScript in themes. A fundamental tool in achieving this modularity is through JavaScript modules.

A key feature of the [Shopify CLI Theme Component plugin](https://github.com/archetype-themes/plugin-theme-component) is its capability to detect JavaScript files and automatically construct an [import map](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/script/type/importmap) as a snippet. This import map snippet can then be integrated into your theme's code.

The backbone of this is the [`import-map.json`](https://github.com/archetype-themes/reference-components/blob/main/importmap.json) file located at the root of the `reference-components` repository. Here is an example of what it looks like:

```json
{
  "imports": {
    "components/*": "components/**/*.js"
  }
}
```

This file defines all imports that can be use across components. It accepts module specifiers with glob patterns or wildcards and resolves JavaScript from URLs or file patterns.

For instance, in the [`icon`](https://github.com/archetype-themes/reference-components/blob/main/components/icon/assets/icon.js) component, a JavaScript module specified in the import map needs to be loaded. This is facilitated through an `import-map.liquid` snippet:

```js
<script type="importmap">
{
  "imports": {
    "components/icon": "{{ 'icon.js' | asset_url }}"
  }
}
</script>
```

You can include this snippet in your theme's layout, typically within the [`layout/theme.liquid`](https://github.com/archetype-themes/reference-theme/blob/main/layout/theme.liquid#L19) file, to ensure all specified modules are correctly loaded.

Keep in mind, an import map simply references modules in the form of a map. A JavaScript module will only be loaded if it is explicitly referenced or imported by a component.