### Component Liquid

Behind the scenes, Liquid files will automatically be compiled to your theme's `snippets/` directory.

Each component is broken down in a specific way. The details below are based on our own approach to developing components, meaning entirely optional. Read on to better understand the anatomy of a component and how we structure our own.

#### Documentation

Each theme component should include a Liquid `comment` tag at the beginning of the file, outlining key information about the component:

```liquid
{% comment %}
  Header section

  Accepts:
  - slot_icons {string} - Slot for icons
  - menu_link_list {string} - Link list to use for the main menu
  - menu_position {'below'|'left'|'center'} - Position of the main menu

  Usage:
  {% render 'section-header' %}
{% endcomment %}
```

The documentation for each component is organized into three main parts:

- **Description**: Explains the component's function.
- **Parameters**: Lists parameters the component accepts, with possible values and their purposes.
- **Usage example**: (Optional) Demonstrates how to use the component within the theme or other components.

This structured approach to documentation ensures that every component is clearly defined, making it easier for developers to learn about and use the theme component in practice.

> **_NOTE_**: Conventions to keep in mind when defining attributes in components:
>
> - If an attribute is of an object type, specify the associated Liquid object.
> - For attributes of any other type, such as strings, separate possible values with a pipe (`|`). For example, use `{'small'|'large'}` to indicate selectable options.

#### Parameter list and order of precedence

The parameter list defines the accepted parameters for each component within the theme. Here's how you can define a parameter list using Liquid:

```liquid
{%- liquid
  assign menu_link_list = menu_link_list | default: section.settings.menu_link_list | default: 'main-menu'
  assign menu_position = menu_position | default: section.settings.menu_position | default: ''
-%}
```

It's vital to manage how data is passed and used effectively in each component. Remember, components should be self-contained snippets, designed to function independently. The order of precedence plays a crucial role in achieving this functionality.

Parameter values are determined through a cascading order:

1. **Directly passed parameter**: First, we check if the parameter has been directly passed to the component. This provides the most specific level of control.
2. **Section/block setting**: If the parameter is not directly passed, the next level checked is the section or block setting. If a setting with a matching ID exists, such as `section.settings.menu_link_list`, its value is used.
3. **Default value**: In the absence of direct parameters or settings, a predefined default value is used. This ensures that every parameter has a value, defaulting to Liquid's `nil` if none is specified.

This cascading system allows each step to be optional. You can choose to enforce a parameter as "required" by omitting a list of fallbacks.

The simplicity of this system allows for more straightforward syntax when referencing the component in your theme. Typically, you can render a component without specifying all parameters:

```liquid
{% render 'section-header' %}
```

However, you can easily override any parameter by passing it directly:

```liquid
{% render 'section-header', menu_link_list: 'some-other-menu' %}
```

This approach not only maintains a clear and organized parameter list but also enhances the legibility and usability of a theme component.

It makes it easier to maintain since the most relevant context for any theme developer jumping into the component's code is at the top of the file, meaning the documentation and the parameter list become the component's API.

> **_NOTE_**: Conventions to keep in mind when defining attributes in components:
>
> - If an attribute is of a boolean value, include `| default: true, allow_false: true` to handle default settings and explicitly allow falsy values.
> - All attributes defined at the top of the file should be the exclusive variables used throughout the file. Avoid direct calls to setting values unless necessary.

#### HTML/Liquid code

In its simplest form, this section is where your component's HTML/Liquid code should be placed.

The content included here depends entirely on the [type of component](#theme-component-types) you are building. For general theme components, you may include any HTML or Liquid markup as needed.

If your component involves integrating JavaScript modules, you should refer to our guidelines in the [Import maps](#import-maps) section to understand our approach to handling JavaScript imports more effectively.
