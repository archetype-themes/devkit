### Components as composable elements

We view components as composable elements, similar to building blocks in a LEGO set. Just like LEGO pieces, these elements can be replaced and swapped out with others.

One idea is to empower developers with a more flexible approach by making parts of components swappable, using the concept of "slots" in Liquid. If a component is designed to accept a ["slot" parameter](#slots-in-components), you can use the Liquid `capture` tag to grab Liquid code—or any value—and pass it as variable content to the component's "slot" parameter.

Also, because components are essentially modular snippets, they can dynamically render other components using the Liquid `render` tag.

It's essential to recognize that these practices are already established in Shopify theme development. Our approach to theme components further leverages these existing mechanisms to simplify and enhance the flexibility of building components, and by extension, entire themes.

#### Slot parameters

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

  render 'section-main-product', slot: blocks
-%}
```

The `section-main-product` component includes a parameter called `slot`. To use this slot, we capture it's content using the Liquid `capture` tag. This slotted content can be any value but is more often a captured "rendered snippet" that is then passed as an attribute to the component. It's then up to the component to output the slot content wherever it needs to go.

If we look at the [`section-main-product`](https://github.com/archetype-themes/reference-components/blob/main/components/section-main-product/section-main-product.liquid) component, you'll see the `slot` parameter being outputted:

```liquid
{%- liquid
  capture product_media_gallery_default
    render 'product-media-gallery'
  endcapture
-%}

<section>
  <div class='main-product__media-gallery'>
    {{- product_media_gallery | default: product_media_gallery_default -}}
  </div>

  <div class='main-product__info'>
    {{- slot -}}
  </div>
</section>
```

You may have also noticed a reference to a `product_media_gallery_default` variable at the top of the file that captures a `product-media-gallery` component. In this case, the `product_media_gallery` parameter is entirely optional and it would fall back to the default value if it isn't specified.

If you're thinking this looks to be another slot for this component, you would be correct! And because of this, you're able to easily swap out the `product_media_gallery` content with your very own, including an entirely different component.

This provides you with a way to modify any components, by passing them parameter values, you may need before you slot them into a component.