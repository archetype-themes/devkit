# Setting Up Your Development Environment

### 1. Setup Shopify CLI and the Theme Component Plugin

We've made it easy to incorporate theme components into your development workflow by building a Shopify CLI plugin that adds a suite of commands accesible via `shopify theme component`.

See the [archetype-themes/plugin-theme-component](https://github.com/archetype-themes/plugin-theme-component?tab=readme-ov-file#getting-started) README for setup details.

### 2. Setup your development store

Just like theme development, you'll need a [development store](https://shopify.dev/docs/apps/tools/development-stores) to preview your code as you work. Use one that you already have or go ahead and create a new one!

### 3. Setup our catalogue of reference components

To best illustrate our vision for components and facilate discussion, we're open-sourcing a small collection of them in the [archetype-themes/reference-components](https://github.com/archetype-themes/reference-components) repo.

We're going to be using these components as part of this guide, so you'll need to:

1. [Clone the repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository) to your dev machine, e.g. `git clone https://github.com/archetype-themes/reference-components.git`
2. [Install the npm dependencies](https://docs.npmjs.com/cli/v10/commands/npm-install) with `npm i`
3. Checkout the `getting-started` branch with `git checkout getting-started-components`

### 4. Create your .env with your dev store details

To streamline Shopify CLI commands and other future steps, make a copy of the `.env.example` file and name it `.env`. Most importantly for this guide, make sure to update the `SHOPIFY_FLAG_STORE` and `SHOPIFY_STORE_PASSWORD` values:

```
SHOPIFY_FLAG_STORE=your-dev-store.myshopify.com
```

>[!WARNING]
> Never commit your .env to version control since it can contain sensitive information

---

### [> Next Step: Code adjustments](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20components/d.%20Code%20adjustments.md)
