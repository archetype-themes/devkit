# The Component Explorer

The Component Explorer is a development environment built directly into the [Shopify CLI plugin](https://github.com/archetype-themes/plugin-theme-component). It enables theme developers to create, develop and test theme components in an isolated environment within the [Shopify theme editor](https://shopify.dev/docs/themes/tools/online-editor).

The Component Explorer becomes the default environment when you run the following command inside of a [components repository](https://github.com/archetype-themes/reference-components):

```bash
shopify theme component dev
```

![2023-11-09 15-25-05](https://github.com/archetype-themes/explorer/assets/4837696/e23acff7-7c28-45e4-923b-5478881013f2)
_^^ Replace with more recent demo_

## Developing components in the Component Explorer

To work with theme components inside of the Component Explorer, you must properly set up a component and ensure that its `setup/` folder is included.

This setup folder should contain a `sections/` and `templates/` folder containing their appropriate files.

### Section folder

The `section/` folder contains the list of sections in which you want to view your component. A section file is structured similarly to a [Shopify theme section](https://shopify.dev/docs/themes/architecture/sections) and typically includes a JSON schema.

### Templates folder

The `templates/` folder contains a list of [JSON templates](https://shopify.dev/docs/themes/architecture/templates/json-templates) in which you want each section viewed. The Component Explorer uses alternate templates to render these sections in the context of JSON templates, and they are structured identically.

### Real-world example

Consider the [`media-with-text`](https://github.com/archetype-themes/reference-components/tree/main/components/section-media-with-text/setup/sections) section component, which uses the structure outlined above to display different versions of the component inside of the Component Explorer. Although its `sections/` folder only contains one section file, you are not limited to a single file.

Here is how we define the [`media-with-text.liquid`](https://github.com/archetype-themes/reference-components/blob/main/components/section-media-with-text/setup/sections/media-with-text.liquid) section file:

```liquid
{% liquid
  capture block
    for block in section.blocks
      case block.type
        when '@app'
          render block
        when 'image'
          render 'block-image', block: block
        when 'video'
          render 'block-video', block: block
        when 'model'
          render 'block-model', block: block, autoplay: true
      endcase
    endfor
  endcapture

  render 'section-media-with-text', slot: block
%}

{% schema %}
{
  "name": "t:labels.media_with_text",
  "max_blocks": 1,
  "settings": []
}
{% endschema %}
```

Within the `templates/` folder, we define an [`index.media-with-text.json`](https://github.com/archetype-themes/reference-components/blob/main/components/section-media-with-text/setup/templates/index.section-media-with-text.json) alternate JSON template to render this section:

```json
{
  "sections": {
    "media_with_text_1": {
      "type": "media-with-text",
      "blocks": {
        "image": {
          "type": "image",
          "settings": {
            "media_crop": "portrait"
          }
        }
      },
      "block_order": ["image"],
      "settings": {
        "full_width": false,
        "media_width": "33",
        "layout": "left",
        "content_alignment": "center",
        "subheading": "Travel Essentials",
        "heading": "Pack for adventure",
        "heading_size": "h2",
        "text": "<p>Your journey begins with the essentials. Our premium travel gear combines style and functionality to accompany you to any destination.</p>",
        "button_text": "Organize in style",
        "color_scheme": "scheme-3"
      }
    },
    "media_with_text_2": {
      "type": "media-with-text",
      "blocks": {
        "video": {
          "type": "video"
        }
      },
      "block_order": ["video"],
      "settings": {
        "full_width": false,
        "media_width": "66",
        "content_alignment": "right",
        "content_position": "bottom",
        "heading": "Unearth wonders",
        "heading_size": "h2",
        "text": "<p>Explore the curated selection of innovations that bring the world closer to you. From the latest tech to timeless crafts, find your next extraordinary discovery.\"</p>",
        "button_text": "Begin your journey",
        "color_scheme": "scheme-1"
      }
    }
  },
  "order": ["media_with_text_1", "media_with_text_2"]
}
```

This structure allows you to develop a component in isolation with various configurations in a single template.

Developing components in isolation also benefits from being able to [test your components](#).
