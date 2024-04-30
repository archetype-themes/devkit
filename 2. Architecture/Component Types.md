### Theme component types

While all theme components are fundamentally modular Liquid snippets, their design and intended use within a Shopify theme can vary. We categorize components based on their specific roles and how they enhance different parts of the theme:

#### Section Components

Section components are robust, reusable parts of Shopify themes that users can manipulate through the theme editor. These components are typically used for larger areas of a page, like headers, footers, or any other content sections.

For example, the [`section-header`](https://github.com/archetype-themes/reference-components/tree/main/components/section-header) component defines the layout and functionality of the site's header section. This would then include other theme components for the store's main navigation and cart icon.

#### Block Components

Block components are smaller, more specific elements that can be nested within section components. They are designed to be customizable within the Shopify theme editor, allowing users to adjust individual blocks of content like text, images, or buttons.

For example, the [`block-model`](https://github.com/archetype-themes/reference-components/tree/main/components/block-model) component defines the output and functionality of a product's 3D model based on whatever `product` object is passed to it.

#### Generic Components

Generic components are versatile and reusable elements that aren't necessarily specific to any part of the theme but can be used in multiple contexts. They are akin to web development's "web components," designed to be plug-and-play across different locations within a theme.

For example, the [`icon`](https://github.com/archetype-themes/reference-components/tree/main/components/icon) component defines the output for a specific icon which can be used in any context, like the header section, the block model, etc.

#### Utility Components

Utility components are designed to provide specific, non-visual functionality that can be used across various parts of a theme. Unlike presentational components, they focus on enhancing a theme's practical capabilities, adding essential features such as performance enhancements and other standard front-end functionality.

For example, the [`font-faces`](https://github.com/archetype-themes/reference-components/tree/main/components/font-faces) component outputs a font preload link based on a given `font` object.