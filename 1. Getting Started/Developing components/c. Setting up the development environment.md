# Setting Up Your Development Environment

### 1. Setup Shopify CLI and the Theme Component Plugin

We've made it easy incorperate theme components into your development workflow by building a Shopify CLI plugin that adds suite of commands accesible via `shopify theme component`.

See the [archetype-themes/plugin-theme-component](https://github.com/archetype-themes/plugin-theme-component) README for setup details.

### 2. Setup our catalogue of reference components

To best illustrate our vision for components and facilate discussion, we're open-sourcing a small collection of them in the [archetype-themes/reference-components](https://github.com/archetype-themes/reference-components) repo.

We're going to be using these components as part of this guide, so you'll need to:

1. [clone the repository](https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository)
2. [Install the npm dependencies](https://docs.npmjs.com/cli/v10/commands/npm-install) with `npm i`
3. Checkout the `getting-started` branch with `git checkout -b getting-started`

### 3. Setup your development store

Just like theme development, you'll need a [development store](https://shopify.dev/docs/apps/tools/development-stores) to preview your code as you work. Use one that you already have or go ahead and create a new one!