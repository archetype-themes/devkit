# Client-side JavaScript with `<is-land>`

For components requiring client-side JavaScript, we adopt the [`is-land`](https://github.com/11ty/is-land) architecture. This approach allows us to specify a loading strategy to control how and when a component's JavaScript is initialized, and allows us to improve performance by being intentional about when JavaScript executes. More details can be found in the `is-land` project's [README](https://github.com/11ty/is-land#readme).

In our implementation, we've created a specific `is-land` component that includes a script tag for the `is-land` JavaScript module. This script is included early in the theme's [`layout/theme.liquid`](https://github.com/archetype-themes/reference-theme/blob/main/layout/theme.liquid#L21) file to ensure it loads and executes before any other dependent component.

For instance, consider our [`cart-note`](https://github.com/archetype-themes/reference-components/blob/main/components/block-cart-note/block-cart-note.liquid) component. We encapsulate the entire component within `<is-land>` tags and use a hydration strategy to control script initialization:

```liquid
<is-land on:visible >
  {% comment %}Cart note Liquid code{% endcomment %}

  <template data-island>
    <script type='module'>
      import 'components/block-cart-note'
    </script>
  </template>
</is-land>
```

In this example, the `on:visible` strategy initializes the module only when the component becomes visible to the user. This strategy is defined in the component's parameter list and can be easily changed to another condition if necessary.

The JavaScript file, [`block-cart-note.js`](https://github.com/archetype-themes/reference-components/blob/main/components/block-cart-note/assets/component.block-cart-note.js), is located in the component's `assets/` directory and is automatically included in the import map to ensure it is properly loaded when referenced.
