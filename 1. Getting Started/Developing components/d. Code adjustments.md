# Code Adjustments

## Develop your component in the explorer

A component isn't truly encapsulated unless it can be loaded and worked on it isolation, which is exactly what the Component Explorer aims to provide!

The following steps outline a straightforward process for developing a component in isolation, such as `components/block-title`.

To begin developing theme components, you will need to open two terminals for the following processes:

**1. Start component development**

First, initiate the component development command and specify the name of the component you want to develop:

```bash
$ shopify theme component dev block-title
```

This command copies the sections and templates from the component's `setup/` directory to the `.explorer/` directory.

**2. Launch Component Explorer**

Next, serve the Component Explorer using the Shopify CLI, specifying the path to the `.explorer/` directory:

```bash
shopify theme dev --path .explorer
```

This step pushes the files of the Component Explorer to Shopify and provides URLs to preview and customize your component.

### Editing the component

For this example, we will demonstrate how to show the vendor of a product from a given text input with dynamic sources support.

**Step 1: Add HTML to output vendor information**

Add the following HTML to output the information of the vendor:

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

**Step 2: Define variables at the top of the file**

At the top of the file, define the following Liquid variables:

```diff
+  assign vendor_enable = block.settings.vendor_enable
+  assign collection_handle = vendor_enable | handleize
+  assign collection_for_vendor = collections[collection_handle]
+  assign vendor_url_default = vendor_enable | url_for_vendor
+  assign vendor_url = collection_for_vendor.url | default: vendor_url_default
```

**Step 3: Update the block settings**

Finally, update the settings of the block in `setup/sections/block-title.liquid` and `setup/templates/product.block-title.json`:

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

At this point, the vendor information should display as expected. Try customizing its value in the theme editor. In the following chapter, we will add tests for the above edits.