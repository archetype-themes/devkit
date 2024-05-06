# Setting up the development environment

1. **Reference theme repository**:
  - Clone the `reference-theme` repository and switch to the `getting-started-theme` branch.
```bash
git clone https://github.com/path/to/reference-theme.git
cd reference-theme
git checkout getting-started-theme
```
2. **Reference components repository**:
  - Similarly, clone the `reference-components` repository and switch to the `getting-started-components` branch.
```bash
git clone https://github.com/path/to/reference-components.git
cd reference-components
git checkout getting-started-components
```
3. **Development store**:
  - Set up a new development store (e.g., `new-theme.myshopify.com`) to preview changes.
4. **Install latest version of components**:
  - Back in your `reference-theme` workspace, install the components from the `getting-started-components` branch using the local path.
```bash
shopify theme component install --components-path="../reference-components"
```

  - Commit and push these changes to update the `getting-started-theme` branch.

```bash
git commit -m "Installed v1 of components"
git push
```
5. **Development store setup**:
  - Connect your GitHub account to the development store and select the `getting-started-theme` branch to publish as the live theme.

> [!NOTE]
>We're using the Shopify Github integration to automatically deploy changes to the development store. This allows us to preview changes in real-time. Learn more about [Shopify's Github integration](https://shopify.dev/themes/tools/github-integration).
