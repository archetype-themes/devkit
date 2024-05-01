# Component locales

Ecommerce websites, like those powered by [Shopify themes](https://shopify.dev/docs/themes), contain common strings of text like `Add to cart` and `Continue shopping`.

The current approach of maintaining this list of strings, and their translations, is typically done by including locale files directly within a theme's codebase.

Gone are those days.

Alongside our [Shopify CLI plugin](https://github.com/archetype-themes/plugin-theme-component), we built [Archetype ecommerce locales](https://github.com/archetype-themes/locales/tree/main) and, as a result, you're now able to add, update, and maintain locales in a single isolated hub of translations that you're then able to inject directly into your theme.
