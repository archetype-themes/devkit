# Setting up your development environment

### 1. Clone and setup repos locally

The “Getting started” branches in our repositories ([getting-started-theme](https://github.com/archetype-themes/reference-theme/tree/getting-started-theme) in `reference-theme` and [getting-started-components](https://github.com/archetype-themes/reference-components/tree/getting-started-components) in `reference-components`) are designed to guide you through the initial setup and development of a new theme using our components.

  - Clone the `reference-theme` [repository](https://github.com/archetype-themes/reference-components) and switch to the `getting-started-theme` branch.
```bash
git clone https://github.com/path/to/reference-theme.git
cd reference-theme
git checkout getting-started-theme
```
  - Similarly, clone the `reference-components` [repository](https://github.com/archetype-themes/reference-theme) and switch to the `getting-started-components` branch.
```bash
git clone https://github.com/path/to/reference-components.git
cd reference-components
git checkout getting-started-components
```
### 2. Setup your development store
  - You'll need a development store to preview your code as you work. Use one that you already have or go ahead and create a new one!

### 3. Setup the Github integration with your shop
  - Open the Shopify admin and navigate to `Online Store` > `Themes`.
  - Click on the `Add theme` button and select `Connect from Github`.
  - Follow the prompts to connect your Github account to the development store.
  - Select the `reference-theme` repository and the `getting-started-theme` branch to publish it as the live theme.
  - Connect your GitHub account to the development store and select the `getting-started-theme` branch.
  - The theme will then get added to your theme library. Publish it to make it live.
  - Share the development store URL with your team to preview changes in real-time.

> [!NOTE]
>We're using the Shopify Github integration to automatically deploy changes to the development store. This allows us to preview changes in real-time. Learn more about [Shopify's Github integration](https://shopify.dev/themes/tools/github-integration).

---

### [> Next Step: Installing updated components](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20themes%20with%20components/d.%20Installing%20updated%20components.md)
