# Install latest version of components

  - Back in your `reference-theme` workspace, install the components from the `getting-started-components` branch using the local path.
```bash
shopify theme component install --components-path="../reference-components"
```

  - Commit and push these changes to update the `getting-started-theme` branch.

```bash
git commit -m "Installed v1 of components"
git push
```