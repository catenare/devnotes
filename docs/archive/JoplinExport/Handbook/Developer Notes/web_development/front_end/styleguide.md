---
title: styleguide
updated: 2020-09-10 22:07:13Z
created: 2020-09-10 22:07:13Z
---

# Styleguide Notes

## CSS/SCSS
* Resources
    * [CSS Architecture](http://bradfrost.com/blog/post/css-architecture-for-design-systems/)
    * [CSS Style Guide](https://cssguidelin.es)
    * [Thoughtful CSS Architecture](https://seesparkbox.com/foundry/thoughtful_css_architecture)

```
There are only two hard things in Computer Science: cache invalidation and naming things.
-- Phil Karlton
```

### Why?
* Working on a team.
* Working on multiple projects and being able to understand the project when you come back to it.
* Keep CSS maintainable.
* Keep stylesheets scalable.
* Documentation for the next developer on the system. Easier to transfer to another developer. Not required to be a mind reader anymore.
    * Code as comments have failed.

### CSS/SCSS Architecture & Styleguide
* Suggestions
    1. Modular - separation between components
    1. Legible - easy to read (think Python pep8)
    1. Clarity over succinctness - clear rather than clever.
    1. Flat - naming not too long
    1. Avoid conflicts - namespacing for components to avoid conflicts

* Naming convention
    * `.cn-{company-name}` - global company name space. Company name not necessary if specific company
    * `.c-` - component `.ui` - component css `.c-ui-slider`
    * `.l-` - layout item - `.l-grid-6`
    * `.is-` or `.has-` - state of the item
    * `.js-` - JavaScript targeting. No style associated. Used for JS targeting (click, etc.)

* BEM
    * Block - Element - Modifier
    * `.cn-c-card__title` - Block is *.cn-c-card* and Element is *__title*
    * `.cn-c-alert--error` - Block *.cn-c-alert* and modifier *--error*

* Organization
    * Base styles
        * Rules for bare elements. Like normalizer. Keep it minimal
    * Objects
        * Focus on structure and layout. No decorative styles.
    * Components
        * Discrete, self-contained units of UI. Button or a carousel. Needs to be self contained. Drop anywhere on a page and it maintains its structure and design. (Name spacing)
    * State
        * Modify the state of a component (selected/not selected), open/close. Rather than adding or removing classes with JS, just change the state class.
    * Themes
        * Alter component (page) to use unique colors, fonts and decorations. Perception rather than structure. Entire page or just a component.
    * Utilities
        * Single purpose styling rule. Created for reuse. Minor changes to an existing component without changing the component. Make a specific instance of a component with a bold title rather than italic title for example.
    * JavaScript Hooks
        * Decouple js-hook classes from styling classes. Disconnect the tie between the two.
    * File organization
        1. Settings: Variables and other settings
        1. Tools: Custom functions and mixins
        1. Generic: Base styles
        1. Elements - Element defaults
        1. Objects - layout and structure
        1. Components - individual components
        1. Overrides - Final rules that might overrule previous rules.

* SCSS rules
    * Limit nesting to 3 layers deep
    * What to nest
        * Modifiers of style block
            * `.cn-c-alert { border: 1px solid gray; &--error { border: 1px solid red;}}` 
        * Media queries
        * Parent selectors
            * All rules for a component in one location
        * States
            * Component states in one location. `hover`, `focus` and `active` states included.
    * Use variables when values are used more than once.

## Forms
* [Design Better Forms](https://uxdesign.cc/design-better-forms-96fadca0f49c)
    * Single column forms
    * Top align labels
    * Group labels with their inputs (put space between inputs)
    * Show all options if under 6 options
    * Resist using placeholders as labels.
    * Options and checkboxes should be placed under each other.
    * Make Call-To-Actions explicit
    * Specify inline-errors for forms.
    * Ditch * and denote optional fields excplicitly
    * Group related information.
* [Web From Usability: Top 10 Recommendations](https://www.nngroup.com/articles/web-form-design/)
    * Keep it short
    * Group related labels and fields
    * Fields in single column
    * Use logiical sequencing
    * Avoid placeholder text
    * Match fields to type and size of input (ie. zip code field should be small)
    * Distinguish between optional and required fields (explicit about what is optional)
    * Explain input or formatting requirements
    * Avoid reset, clear buttons. At least reduce visually prominence.
    * Provide visible and specific error messages.
