---
category: Components
status: Use with caution
component:
  status: ready
  package: usa-combo-box
  dependencies:
implementation:
  initProps:
    - property: "`required`"
      element: select
      description: The combo box component will be required in terms of native form validation.
    - property: "`disabled`"
      element: select
      description: The combo box component will be disabled / read-only. You can re-enable it by executing the enable procedure on the component.
    - property: "`data-placeholder`"
      element: .usa-combo-box
      description: To update the placeholder text of the combo box, use the `data-placeholder` attribute. We recommend using a label or hint instead of a placeholder.
    - property: "`data-default-value`"
      element: .usa-combo-box
      description: The combo box will set this value as the default selection if it is found within the select options.
  props:
    - property: "`data-filter`"
      element: .usa-combo-box
      description: The combo box will use this regular expression to filter the combo box options. You are declaring a case insensitive match over the entire option text, which means `^` and `$` are added automatically. You can specify the inputted query with `{{query}}`. You can also declare a custom query filter as a data property as well, which can be used in the custom filter (`data-number-filter="[0-9]"` and then using `data-filter="{{numberFilter}}.*"`). The default filter is `.*{{query}}.*`, which is a simple "find anywhere within the option" text.
  procedures:
    - procedure: "`enable`"
      parameters: .usa-combo-box
      description: The combo box component will be enabled.
    - procedure: "`disable`"
      parameters: .usa-combo-box
      description: The combo box component will be disabled / read-only.
layout: component
lead: A combo box helps users select an item from a large list of options.
permalink: /components/combo-box/
redirect_from:
  - /form-controls/03-combo-box/
subnav:
- text: Preview
  href: '#combo-box-preview'
- text: Code
  href: '#combo-box-code'
- text: Guidance
  href: '#combo-box-guidance'
- text: Package
  href: '#combo-box-package'
- text: Latest updates
  href: '#changelog'
tags:
  - form
  - forms
  - form controls
  - input
  - select
title: Combo box
type: component
alert: true
alert-class: info
alert-heading: Current accessibility issues
alert-content: In late 2022, we found some combo box <a href="#accessibility-combo-box">usability issues</a> when we were testing with people who use screen readers and alternative input devices. For more information, see <a href="https://github.com/uswds/uswds-site/issues/1898">the issue on GitHub</a>.
changelog:
  key: component-combo-box
---

