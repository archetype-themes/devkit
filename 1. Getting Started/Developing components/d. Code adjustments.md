# Code Adjustments

A component isn't truly encapsulated unless it can be loaded and worked on in isolation, which is exactly what the Component Explorer aims to provide!

The following steps outline a straightforward process for developing a component in isolation, such as `components/block-title` and `components/variant-sku`.

## Develop your components in the component explorer

To begin developing theme components, you will need to open two terminals for the following processes:

**1. Start component development**

First, initiate the component development command and specify the name of the component you want to develop:

```bash
shopify theme component dev
```

This command builds your components, copies the sections and templates from the component's `setup/` directory to the `.explorer/` directory, and starts up a watcher for file changes.

You now have a fully assembled component explorer theme inside the `.explorer` directory

**2. Launch Component Explorer**

Next, serve the Component Explorer using the Shopify CLI, specifying the path to the `.explorer` directory:

```bash
shopify theme dev --path .explorer --store [your-shop.myshopify.com]
```

This step pushes the files of the Component Explorer to Shopify and provides URLs to preview and customize your component.

<img width="1159" alt="image" src="https://github.com/archetype-themes/devkit/assets/4837696/b31c9eeb-b5f5-4031-a499-12b41a275fe4">

Click through to preview the `block-title` component


## Update your component

For this example, we will demonstrate how to show the vendor of a product from a given text input with dynamic sources support.

**Step 1: Add HTML to output vendor information**

Replace the main HTML contents of the `components/block-title/block-title.liquid` with the following allow for product vendor to render:

```liquid
<div class="block-title" data-section-id="{{ section.id }}" {{ block.shopify_attributes }}>
  <h1 class="h2 block-title__heading">
    {{- title -}}
  </h1>

 {%- if vendor_enable or sku_enable -%}
   <div class="block-title__vendor-sku">
     {%- if vendor_enable != blank -%}
       <a class="block-title__vendor" href="{{ vendor_url }}">
         {{- vendor_enable -}}
       </a>
     {%- endif -%}
   </div>
 {%- endif -%}
</div>
```

**Step 2: Include other components**

Your component can include other components, such as `variant-sku`, which is an interactive one that changes depending on the selected variant. Replace the contents of your HTML to include the `variant-sku` component.

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
          {%- render 'variant-sku' -%}
        </div>
      {%- endif -%}
    </div>
  {%- endif -%}
</div>
```

**Step 2: Define variables at the top of the file**

Above the HTML, replace the contents of the `{%- liquid -%}` tag to declare the following Liquid variables:

```liquid
{%- liquid
  assign sku_enable = sku_enable | default: block.settings.sku_enable | default: false
  assign vendor_enable = vendor_enable | default: block.settings.vendor_enable | default: false
  assign title_default = 'labels.example_product' | t
  assign title = product.title | default: title_default
  assign collection_handle = product.vendor | handleize
  assign collection_for_vendor = collections[collection_handle]
  assign vendor_url_default = product.vendor | url_for_vendor
  assign vendor_url = collection_for_vendor.url | default: vendor_url_default
-%}

```

**Step 3: Update the component parameter docs**

We want it to be clear what parameters are available for use with this components, so let's update the `{% comment %}` at the top of the file with our two new parameters `sku_enable` and `vendor_enable`:

```liquid
{%- comment -%}
  Renders the product title

  Accepts:
  - block {block} - Block object
  - product {product} - Product object
  - sku_enable {boolean} - Show or hide the product sku
  - vendor_enable {boolean} - Show or hide the vendor

  Usage:
  {% render 'block-title', block: block %}
{%- endcomment -%}

```

**Step 4: Manually set your component params**

One way of showing the vendor is to set `vendor_enable` directly when the component is included. To do that we can update the `setup/sections/block-title.liquid` file, which is only used inside the component explorer experience to properly render our component. To find out more about setup files, see [Theme Components File Structure](https://github.com/archetype-themes/devkit/blob/main/2.%20Architecture/Theme%20Components/File%20Structure.md).

```liquid
{%- liquid
  for block in section.blocks
    case block.type
      when 'title'
        render 'block-title', block: block, vendor_enable: true
    endcase
  endfor
-%}
```

You should now see the product vendor rendered inside the component preview

**Step 5: Update the component to render using block settings**

If you look back at our parameter assignements, you can see that we added some helpful defaults that reference block settings if they are available. Instead of statically setting component parameters, let's make them set via block settings. 

Let's remove the static parameter value that's set in `setup/sections/block-title.liquid`:

```liquid
{%- liquid
  for block in section.blocks
    case block.type
      when 'title'
        render 'block-title', block: block
    endcase
  endfor
-%}
```

Update the settings of the block in `setup/sections/block-title.liquid`:

```liquid
{% schema %}
{
  "name": "t:labels.product",
  "settings": [],
  "blocks": [
    {
      "type": "title",
      "name": "t:labels.title",
      "limit": 1,
      "settings": [
        {
          "type": "checkbox",
          "id": "vendor_enable",
          "label": "t:actions.show_vendor"
        },
        {
          "type": "checkbox",
          "id": "sku_enable",
          "label": "t:actions.show_sku"
        }
      ]
    }
  ]
}
{% endschema %}
```

And the values of those settings inside the `setup/templates/product.block-title.json`:

```json
{
  "sections": {
    "block_title": {
      "type": "block-title",
      "blocks": {
        "title_1": {
          "type": "title",
          "settings": {
            "vendor_enable": true,
            "sku_enable": true
          }
        }
      },
      "block_order": ["title_1"]
    }
  },
  "order": ["block_title"]
}
```

**Step 4: Style your component**

Add the following CSS to the bottom of the `main.css` file of your component to make sure there is some space between the SKU and vendor elements:

```css
.block-title__sku,
.block-title__vendor {
  display: inline-block;
  margin-right: var(--size-5);
}
```


At this point, the sku and vendor information should display as expected. Try customizing its value in the theme editor. In the following chapter, we will add tests for the above edits.

---

### [> Next Step: Writing tests](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20components/e.%20Writing%20tests.md)
