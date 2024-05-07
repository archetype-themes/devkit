# Developing Themes with Components

Welcome to the "Developing Themes with Components" guide. This resource is designed to help you streamline Shopify theme development using the Archetype Developer Kit, enhancing your projects with modular and reusable components.

Our approach, similar to working with Dawn, uses familiar tools and workflows, making it easy to integrate modern, component-based architecture. This method not only simplifies development and enriches customization but also facilitates easier theme updates across your theme catalogue, ensuring your themes remain adaptable and maintainable.

For more details about the architecture of themes built with components, check out [Introduction to Devkit Theme Architecture]().

## Overview

This document provides a step-by-step guide on developing Shopify themes using components from the Archetype Developer Kit, emphasizing integration and customization. Here’s what we’ll cover:

- **Reviewing Design Specifications:** We begin by ensuring a thorough understanding of the theme's visual and functional requirements based on the provided design specifications.
- **Setting Up the Development Environment:** This step involves configuring a development store for testing, cloning the reference-theme and reference-components repositories, along with any necessary additional tools and setups.
- **Installing updated components:** We'll demonstrate how easy it is to leverage updates to the component library in your theme by running a simple install command.
- **Code Adjustments:** This phase includes updating components to support new design features and integrating locales into the theme editor settings.
- **Customizations:** This phase involves adding a layer of customization to the components once they're a part of the theme. We can accomplish this through custom CSS and CSS variable overrides in the theme's layout files. In our example, we'll be adding some custom CSS to the theme.
- **Incorporating Best Practices:** We emphasize applying best coding practices throughout the development process to ensure high quality and maintainability.
- **Committing Changes and Review:** Details on making changes using GitHub and setting up branch previews for team review.

By the end of this document, you will know how to integrate and customize components for Shopify theme development. You'll manage a development environment, adjust components to fit design specs, and implement best practices for robust themes. You'll also handle GitHub version control, review processes, and deploy your theme to a live Shopify store, ensuring your development skills meet current e-commerce standards.

The “Getting started” branches in our repositories ([getting-started-theme](https://github.com/archetype-themes/reference-theme/tree/getting-started-theme) in `reference-theme` and [getting-started-components](https://github.com/archetype-themes/reference-components/tree/getting-started-components) in `reference-components`) are designed to guide you through the initial setup and development of a new theme using our components.
