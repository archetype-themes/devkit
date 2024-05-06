Going back to the reference-theme workspace, open up the `main-product` section file so we can review what the content of this section looks like. There’s a `block-title` block being rendered, which is the perfect place for our new information.

Also within this section file is the schema for all of the section and block settings. Locate the title block and add the two new settings for vendor and SKU. We’ve also provided the translations for these new settings. To learn more about how we work with translations, see our [guide on theme locales](https://github.com/archetype-themes/locales).

```
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

The development store for your project will allow you to preview any changes automatically once they’re pushed to the `getting-started-theme` branch. In addition, you can use Shopify CLI to deploy your work-in-progress changes to a development theme.

At this point, the block settings will show in the theme editor but we need to edit our title block so that it can leverage these new settings and display the relevant information.

Open your reference-components workspace and locate the `block-title` component file. Following the best practices outlined in the [Developing with Components guide](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20components/e.%20Incorperation%20best%20practices.md), it’s time to make some updates to this component.

Assign new variables for the `vendor_enable` and `sku_enable` block settings.

```
assign vendor_enable = block.settings.vendor_enable
assign sku_enable = block.settings.sku_enable
```

Let’s add the liquid and HTML markup just below the title within the block-title div in order to render these variables if they exist.

```
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

NOTE: In this chunk of code you can see a reference to the 'variant-sku' component which is a part of reference-components.

Commit these changes to your `getting-started-components` branch `git commit -m “Adds support for vendor and SKU”`.
Switch to the reference-theme workspace and run the install command again so we can update our theme with these changes. If you’re still deploying your theme to the development theme, you should be able to preview these changes instantly. Visit the product template, click into the title block, and you can adjust the settings to hide/show the vendor and SKU.

These changes can now be committed and pushed to the `getting-started-theme` branch, which will flow to the development store for your theme.
This concludes the feature building phase.
