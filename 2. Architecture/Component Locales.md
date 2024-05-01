# Component locales

Ecommerce websites, like those powered by [Shopify themes](https://shopify.dev/docs/themes), contain common strings of text like `Add to cart` and `Continue shopping`.

The current approach of maintaining this list of strings, and their translations, is typically done by including locale files directly within a theme's codebase.

## Archetype ecommerce locales

We built [Archetype ecommerce locales](https://github.com/archetype-themes/locales/tree/main) which allows you to add, update, and maintain locales in a single isolated hub of translations.

As you create and develop new components, you're able to reference locales in the exact same way you would in any Shopify theme:

```liquid
{{ 'actions.add_to_cart' | t }}
```

## Pointing to a different locales repository

When running commands for developing or installing theme components, the locales are injected directly into your theme's `locales/` directory as individual locale files.

The default repository that the CLI plugin points to is https://github.com/archetype-themes/locales.git. However, this can be modified by specifying a different path for the `--locales-path` command flag:

```bash
shopify theme component install --locales-path="https://github.com/{organization}/custom-locales.git"
```

> [!NOTE]
> You can also specify a local path like so: `--locales-path="/Users/{user}/locales"`.
