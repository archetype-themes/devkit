# Setting up the development environment

1. **Clone and setup repos locally**:

The “Getting started” branches in our repositories ([getting-started-theme](https://github.com/archetype-themes/reference-theme/tree/getting-started-theme) in `reference-theme` and [getting-started-components](https://github.com/archetype-themes/reference-components/tree/getting-started-components) in `reference-components`) are designed to guide you through the initial setup and development of a new theme using our components.

  - Clone the `reference-theme` [repository](https://github.com/archetype-themes/reference-components) and switch to the `getting-started-theme` branch.
```bash
git clone https://github.com/path/to/reference-theme.git
cd reference-theme
git checkout getting-started-theme
```
1. **Reference components repository**:
  - Similarly, clone the `reference-components` [repository](https://github.com/archetype-themes/reference-theme) and switch to the `getting-started-components` branch.
```bash
git clone https://github.com/path/to/reference-components.git
cd reference-components
git checkout getting-started-components
```
1. **Development store**:
  - Set up a new development store (e.g., `new-theme.myshopify.com`) to preview changes.

2. **Development store setup**:
  - Connect your GitHub account to the development store and select the `getting-started-theme` branch to publish as the live theme.

> [!NOTE]
>We're using the Shopify Github integration to automatically deploy changes to the development store. This allows us to preview changes in real-time. Learn more about [Shopify's Github integration](https://shopify.dev/themes/tools/github-integration).
