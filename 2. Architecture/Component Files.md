# Component Files

The `reference-components` repository contains all assets associated to components, including any common scripts and styles that can be used across any one of them.

The only required folder is `components/`, both `script/` and `styles/` are optional. See the repository file structure below:

```
📂 reference-components/
├─ 📂 components/
│ ├─ 📂 my-component/
│ │ ├─ 📂 assets/
│ │ │ ├─ custom-icon.svg
│ │ │ ├─ my-component.js
│ │ ├─ 📂 setup/
│ │ │ ├─ 📂 sections/
│ │ │ │ ├─ my-component.liquid
│ │ │ ├─ 📂 templates/
│ │ │ │ ├─ index.my-component.json
│ │ │ │ ├─ product.my-component.json
│ │ ├─ 📂 tests/
│ │ │ ├─ my-component.spec.js
│ │ ├─ my-component.css
│ │ └─ my-component.liquid
├─ 📂 scripts/
└─ 📂 styles/
```

- `components/`: Contains all your components.
  - `assets/`: Asset files associated to the component. Typically contains assets like JavaScript and SVG files that require a transformation step.
  - `setup/`: Used in conjunction with the component explorer to preview the component.
    - `section/`: The section (and its JSON schema) that you want to view the component in.
    - `templates/`: The JSON templates that you want to view the component in.
  - `tests/`: Test files for the component. Uses [Playwright](https://playwright.dev/) to run tests.
  - `{component}.css`: Entrypoint for the component's CSS. Other CSS files can be added in the root directory.
  - `{component}.liquid`: Component Liquid file that gets generated into a snippet when installed in the theme.
- `scripts/`: Contains common scripts that components can reference.
- `styles/`: Contains common styles that components can reference.

> **_NOTE:_** Behind the scenes, any asset files added to your components will automatically be compiled to your theme's `assets/` directory. Similarly, any Liquid files will automatically be compiled to the `snippets/` directory.

#### Liquid component file

Each component directory must include a Liquid component file, which serves as the essential entry point for the component. Upon installing a component into a theme, the Liquid component file will be generated as a separate snippet file.

It is common practice to name the Liquid component file after the component directory itself. For example, a component named `my-component` would typically have a corresponding Liquid file named `my-component/my-component.liquid`. However, this naming convention is not enforced.

Other than the Liquid component file, all other files within the component directory are optional.