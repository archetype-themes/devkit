In one workspace, clone the reference-theme repository and pull the latest changes from the `main` branch. Then check out the `getting-started-theme` branch.

In another workspace, clone the reference-components repository and pull the latest changes from `main`. Then check out the `getting-started-components` branch.

For your team and you to preview changes to the project, you’ll want to create a new development store for the theme ex. new-theme.myshopify.com
Going back into your reference-theme workspace, install the components based on the `getting-started-components` state.

```
shopify theme component install --components-path="../reference-components"

Specifying a local path to our reference-components folder
```

Theme files will now get updated with all of the components and their respective assets. You can commit these changes `git commit -m “Installed v1 of components”`. Then push them to the remote repository so the `getting-started-theme` branch gets updated.

Revisit the development store and add a new theme using the Github integration by connecting your Github account and selecting the `getting-started-theme` branch. Publish this theme as the live theme for the shop
