# Components as composable elements

We view components as composable elements, similar to building blocks in a LEGO set. Just like LEGO pieces, these elements can be replaced and swapped out with others.

One idea is to empower developers with a more flexible approach by making parts of components swappable, using the concept of "slots" in Liquid. If a component is designed to accept a ["slot" parameter](#slot-parameters), you can use the Liquid `capture` tag to grab Liquid code—or any value—and pass it as variable content to the component's "slot" parameter.

Also, because components are essentially modular snippets, they can dynamically render other components using the Liquid `render` tag.

It's essential to recognize that these practices are already established in Shopify theme development. Our approach to theme components further leverages these existing mechanisms to simplify and enhance the flexibility of building components, and by extension, entire themes.

## Slot parameters

Slots are fundamentally "placeholder areas" in which you can _slot_ in content.

Slots enable components to display variable content in designated areas, ensuring that child content is self-contained. This setup allows the parent component to operate without having to manage configurations for both itself and its child components. When possible, components, especially section components, should be built to allow you to slot content into them, providing a flexible way to modify components by passing attribute values that can be adjusted before slotting them into a component.

For example, in the reference theme, the [`main-product`](https://github.com/archetype-themes/reference-theme/blob/main/sections/main-product.liquid) section defines its JSON schema with a set of blocks. In Liquid, it then captures this list of blocks and injects them into a designated slot location within the `section-main-product` component:

```liquid
{%- liquid
  capture blocks
    for block in section.blocks
      case block.type
        when '@app'
          render block
        when 'description'
          render 'block-product-description', block: block
        when 'variant_picker'
          render 'block-variant-picker', block: block
        when 'buy_buttons'
          render 'block-buy-buttons', block: block
        when 'title'
          render 'block-title', block: block
        when 'price'
          render 'block-price', block: block
      endcase
    endfor
  endcapture

  render 'section-main-product', slot_product_blocks: blocks
-%}
```

The `section-main-product` component includes a parameter called `slot_product_blocks`. To use this slot, we capture it's content using the Liquid `capture` tag. This slotted content can be any value but is more often a captured "rendered snippet" that is then passed as an attribute to the component. It's then up to the component to output the slot content wherever it needs to go.

If we look at the [`section-main-product`](https://github.com/archetype-themes/reference-components/blob/main/components/section-main-product/section-main-product.liquid) component, you'll see the `slot_product_blocks` parameter being outputted:

```liquid
<section>
  <div class="main-product__media-gallery">
    {%- if slot_product_gallery != blank -%}
      {{ slot_product_gallery }}
    {%- else -%}
      {%- render 'product-media-gallery' -%}
    {%- endif -%}
  </div>

  <div class="main-product__info">
    {{- slot_product_blocks -}}
  </div>
</section>
```

You may have seen a second slot for the product gallery: `slot_product_gallery`. Because of this, you're able to easily swap out the product gallery with whatever content you choose, including an entirely different component! A parameter, like this one, is entirely optional and it would fall back to the default render within the component if it isn't specified.

## Modifying components before slotting them in

Say we have a custom product gallery component that we created that we know we want to include as part of the `section-main-product` component defined above. And as part of that, we want to ensure a few of its parameter values are set, we can write the following Liquid code:

```liquid
{%- liquid
  capture product_media_gallery
    render 'some-custom-media-gallery', layout: 'stacked', enable_video: section.setting.enable_video
  endcapture

  render 'section-main-product', slot_product_gallery: product_media_gallery
-%}

{% schema %}
{
  "name": "t:labels.product",
  "settings": [
     {
      "type": "checkbox",
      "id": "enable_video",
      "label": "Enable video",
      "default": true
    }
  ]
}
{% endschema %}
```

This mechanism provides you with a way to modify any component, by passing it parameter values, you may need before you slot them into another component.

Keep in mind that these parameter values don't need to be hardcoded when passing them to the component, and the approach you take will vary depending on the theme that you're building. In the example above, we leverage a section setting to update the value of `enable_video` but a hardcoded value for `layout`. The amount of flexibility you provide to a merchant is entirely up to you!
