# Code adjustments

This section details how to integrate new settings for displaying vendor and SKU information within the `main-product` section based on the new design requirements.

## Accessing the main product section file
1. **Navigate to your workspace**: return to the `reference-theme` workspace.
2. **Open the `main-product` section file**: This file contains the `block-title` block, which we'll use to add new information.

## Modifying the schema

Within the `main-product` section file:
- **Find the title block**: This is where we'll add new settings.
- **Insert new settings**: Add settings for vendor and SKU display. Here is the updated JSON schema:
```json
{
  "type": "title",
  "name": "t:labels.title",
  "limit": 1,
  "settings": [
    {
      "type": "inline_richtext",
      "id": "vendor_enable",
      "label": "t:actions.show_vendor",
      "default": "{{ product.vendor }}"
    },
    {
      "type": "checkbox",
      "id": "sku_enable",
      "label": "t:actions.show_sku",
      "default": true
    }
  ]
},
```

> [!NOTE]
> Ensure all new settings are accompanied by appropriate translations. For guidance on working with translations, consult our [guide on theme locales](https://github.com/archetype-themes/locales).

## Previewing changes

- **Development store**: Your project's development store allows you to automatically preview any changes once they are pushed to the `getting-started-theme` branch.
- **Shopify CLI**: Deploy your work-in-progress changes to a development theme using Shopify CLI for instant previews.

## Updating the block title component

1. **Open your `reference-components` workspace**: locate the `block-title` component file.
2. **Assign new variables**:
```liquid
assign vendor_enable = block.settings.vendor_enable
assign sku_enable = block.settings.sku_enable
```
3. **Add Liquid and HTML markup**:
```liquid
{%- if vendor_enable or sku_enable -%}
  <div class="block-title__vendor-sku">
    {%- if vendor_enable != blank -%}
      <a class="block-title__vendor" href="{{ vendor_url }}">
        {{- vendor_enable -}}
      </a>
    {%- endif -%}

    {%- if sku_enable -%}
      <div class="block-title__sku">
        {%- render 'variant-sku', variant: current_variant -%}
      </div>
    {%- endif -%}
  </div>
{%- endif -%}
```

> [!NOTE]
> This code includes a reference to the [`variant-sku`](https://github.com/archetype-themes/reference-components/blob/main/components/variant-sku) component.

## Committing and deploying changes

- **Commit changes**: `git commit -m "Adds support for vendor and SKU"`.
- **Update theme**: Run the install command again in the reference-theme workspace to update the theme with these changes.
- **Preview and adjust**: Visit the product template in the development store, click into the title block, and adjust the settings to hide/show the vendor and SKU.

This concludes our code adjustments. By following these steps, you ensure that your theme components are not only functional but also aligned with the latest design specifications and user requirements.
