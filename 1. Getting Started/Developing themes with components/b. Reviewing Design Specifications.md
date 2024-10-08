# Reviewing design specifications in Figma

>[!TIP]
> The Figma file that accompanies this preview and getting started guide are available for free in Figma Community. [Click here to access it.](https://www.figma.com/community/file/1425140095049949991/devkit-preview)
>
> [Revisit our guide on using Figma to inspect components](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20components/b.%20Reviewing%20Design%20Specifications.md) 


The Shopify Theme components design system in Figma is broken down into 3 layers:

1. Styles; where we are leveraging Figma's styles and variables features to create our design building blocks. We included a sample of the reference demo store that makes up a basic purchase flow for one of our themes.
2. Components; reusable layout configurations that can be used within sections in their base, or modified forms.
3. Sections; section-based components. These include variables and boolean operations that are mapped to our editor setting configurations, and therefore represent these sections in an accurate manner.
   
When selecting a component in the Figma file, you’ll see a component preview, a link to the main component, as well as any links to relevant documentation and designers notes.

Inspecting Components and Styles
The component playground appears in the inspect panel when a component instance is selected. Use the playground to experiment with the component’s different properties without changing the actual design. To open the component playground in Dev Mode:

Select a component instance on the canvas.
Click Open in playground in the Inspect panel.

Example of a design - dev workflow where the system can be leveraged:

1. **Open Figma design specs**: review the design requirements provided by the designer using Dev Mode in Figma.
2. **Component adjustments**: Design is requesting new features such as displaying a new block - product vendor below the product title.
3. **Customizations**: In addition, Design is requesting that we update the styles for the buy buttons and make the element containing the product details sticky.

---

### [> Next Step: Setting up the development environment](https://github.com/archetype-themes/devkit/blob/main/1.%20Getting%20Started/Developing%20themes%20with%20components/c.%20Setting%20up%20the%20development%20environment.md)
