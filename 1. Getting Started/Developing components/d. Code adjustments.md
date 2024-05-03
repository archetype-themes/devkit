# Code Adjustments

## Develop your component in the explorer

A component isn't truly encapsulated unless it can be loaded and worked on it isolation, which is exactly what the Component Explorer aims to provide!

The following steps outline a straightforward process for developing a component in Isolation, such as `components/block-title`.

### Start the component development commands

You will need two terminals to run the following processes.

First, start the component dev command and provide the name of the component to develop.

```bash
$ shopify theme component dev block-title
```

This will copy the sections and templates from the component’s setup/ directory to the .explorer/ directory.

Second, serve the component explorer theme using the Shopify CLI, specifying the theme’s path.

```bash
shopify theme dev --path .explorer
```

This will push the files of the component explorer theme to Shopify and provide URLs to preview and customize it.

### Editing the component

For this example we will show the vendor of the product from a given text input with dynamic sources support.

First, we add the HTML to output the information of the vendor.

```diff
<div class="block-title" data-section-id="{{ section.id }}" {{ block.shopify_attributes }}>
  <h1 class="h2 block-title__heading">
    {{- title -}}
  </h1>

- {%- if sku_enable -%}
+ {%- if vendor_enable or sku_enable -%}
    <div class="block-title__vendor-sku">
+     {%- if vendor_enable != blank -%}
+       <a class="block-title__vendor" href="{{ vendor_url }}">
+         {{- vendor_enable -}}
+       </a>
+     {%- endif -%}
      {%- if sku_enable -%}
        <div class="block-title__sku">
          {%- render 'variant-sku', variant: current_variant -%}
        </div>
      {%- endif -%}
    </div>
  {%- endif -%}
</div>
```

Second, on the top of the file define the following variables.

```diff
+  assign vendor_enable = block.settings.vendor_enable
+  assign collection_handle = vendor_enable | handleize
+  assign collection_for_vendor = collections[collection_handle]
+  assign vendor_url_default = vendor_enable | url_for_vendor
+  assign vendor_url = collection_for_vendor.url | default: vendor_url_default
```

Third, update the settings of the block in setup/sections/block-title.liquid and setup/templates/product.block.title-json

```diff
settings: {
+  {
+    "type": "inline_richtext",
+    "id": "vendor_enable",
+    "label": "t:actions.show_vendor"
+  },
```

```diff
"blocks": {
  "title_1": {
    "type": "title",
    "settings": {
+     "vendor_enable": "{{ product.vendor }}"
    }
  }
}

```

At this point, the vendor should be showing as expected; try customizing its value in the theme editor. In the following chapter, we will add tests for the above edits.

