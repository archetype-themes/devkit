# Custom elements

Custom elements are the foundational blocks that 99% of e-commerce stores use under the hood. They're small pieces of functionality that make up the larger parts of a storefront that you can, most importantly, compose together.

The idea is that we're able build a set of HTML custom elements that we can leverage in all themes. You can have custom elements for anything really—sliders, drawers, popups, etc. but these custom elements can also be much more granular, e.g. a [cart icon](https://github.com/archetype-themes/reference-components/blob/main/components/cart-icon/assets/component.cart-icon.js#L12-L15) that shows the number of products in a buyer's cart and updates when that number changes, or a product block that [listens for an event](https://github.com/archetype-themes/reference-components/blob/main/components/variant-sku/assets/component.variant-sku.js) whenever the variant is changed.

You can find more detailed information about custom elements on the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_custom_elements).
