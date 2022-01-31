---
permalink: /design-tokens/
layout: styleguide
title: Design tokens
category: Design tokens
lead: USWDS visual design is based on consistent palettes of typography, spacing units, color, and other discrete elements of style we call **design tokens**{:.font-lang-8}.
type: docs
subnav:
  - text: Introducing design tokens
    href: '#introducing-design-tokens'
  - text: Keys and values
    href: '#keys-and-values'
  - text: Using design tokens
    href: '#using-design-tokens'
---

{{ page.collection | slugify }}

## Introducing design tokens

Anything we see on a website is built from elements of style: color, spacing, typography, line height, and opacity. The CSS rules associated with these elements can accept a broad continuum of values — in the case of color, there are over 16 million separate colors in the RGB color space. Font size, line height, spacing, and others can accept a similarly wide range of values.

This degree of choice can slow down design work and make communication between designer and developer unnecessarily granular. USWDS seeks to maximize design efficiency and improve communication with **design tokens**: the discrete palettes of values from which we base all our visual design.

Design tokens are a limited set of discrete options, just like a scale of musical notes is drawn from the spectrum of all possible frequencies. Or like the presets on a car radio — not every option, just a specific selection.

{:.padding-y-2}
![continuous and tokenized values]({{ site.baseurl }}/assets/img/design-tokens/continuous-v-token.svg){: role="img"}

### Example: Measure (line length)
For example, measure (or line length) expressed with the `max-width` CSS property can accept any value in units like `em`, `rem`, `ch`, `ex`, and `px` to at least two decimal places. USWDS limits itself to 7 [measure]({{ site.baseurl }}/design-tokens/typesetting/measure/){:.token} tokens:

{:.site-table}
| token   | value
| ---     | ---
|`1`      | `44ex`
|`2`      | `60ex`
|`3`      | `64ex`
|`4`      | `68ex`
|`5`      | `72ex`
|`6`      | `88ex`
|`'none'` | no max width

Anything built using USWDS will use one of these 7 [measure]({{ site.baseurl }}/design-tokens/typesetting/measure/){:.token} tokens when specifying measure.

## Keys and values
You can think of a design token as a **key** that unlocks a specific **value**. Often, the specific value is less important than its effect. Each token is a quoted string or, with only the exceptions of `1px` and `2px`, a unitless number — and the mechanism by which the final display value is unlocked is a **function**, **mixin**, or **utility class**.

We can't include tokens directly in our Sass, like `max-width: 1`, rather we use a helper function like `max-width: measure(1)` or a mixin like `@include u-measure(1)`. All USWDS design tokens have helper mixins and functions to use them in component Sass.

{: .site-note }
**Note:** We do not include the token's value directly into our Sass rules.

### Example: Tokens in settings and component Sass

Tokens can, themselves, be expressed as variables. And this is how most USWDS theme settings work. For instance, the following is an example of theme settings from `_uswds-theme-spacing.scss` showing settings variables assigned spacing unit tokens:

```
$theme-grid-container-max-width:    'desktop';
$theme-site-margins-breakpoint:     'desktop';
$theme-site-margins-width:          4;
$theme-site-margins-mobile-width:   2;
```

USWDS component Sass uses those variableized tokens to build component styles:

```
.usa-example {
  @include u-padding-x($theme-site-margins-mobile-width);
  max-width: units($theme-grid-container-max-width);

  @include at-media($theme-site-margins-breakpoint) {
    @include u-padding-x($theme-site-margins-width);
  }
}
```

This is the functional equivalent of:

```
.usa-example {
  @include u-padding-x(2);
  max-width: units('desktop');

  @include at-media('desktop') {
    @include u-padding-x(4);
  }
}
```

Which, if `$theme-respect-user-font-size` is set to true would output something like:

```
.usa-example {
  padding-left: 1rem;
  padding-right: 1rem;
  max-width: 64rem;
}

@media screen and (min-width: 64em) {
  .usa-example {
    padding-left: 2rem;
    padding-right: 2rem;
  }
}
```

In general, USWDS sets variables with tokens, and passes those variables into functions and mixins in the source Sass.

## Using design tokens

Use design tokens directly to set the value of settings variables in USWDS theme settings files, like `$theme-grid-container-max-width: 'desktop'`. Otherwise, use functions, mixins, or utility classes as in the examples below. See individual design token section for more details.

### Color
<div class="site-table-wrapper">
  <table class="usa-table--borderless site-table-responsive">
    <thead>
      <tr>
        <th scope="col" class="tablet:maxw-card-lg">Token</th>
        <th scope="col">Function</th>
        <th scope="col">Mixin</th>
        <th scope="col">Utility class</th>
      </tr>
    </thead>
    <tbody class="font-mono-2xs">
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            <a href="{{ site.baseurl }}/design-tokens/color/" class="token">color</a>
          </span>
        </th>
        <td data-title="Function">
          <span>
            color(<a href="{{ site.baseurl }}/design-tokens/color/" class="token">color</a>)
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-border(<a href="{{ site.baseurl }}/design-tokens/color/" class="token">color</a>)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .border-<a href="{{ site.baseurl }}/design-tokens/color/" class="token">color</a>
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'red-warm-50'
          </span>
        </th>
        <td data-title="Function">
          <span>
            color('red-warm-50')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-border('red-warm-50')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .border-red-warm-50
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'red-warm-50v'
          </span>
        </th>
        <td data-title="Function">
          <span>
            color('red-warm-50v')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-border('red-warm-50v')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .border-red-warm-50v
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'primary-vivid'
          </span>
        </th>
        <td data-title="Function">
          <span>
            color('primary-vivid')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-text('primary-vivid')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .text-primary-vivid
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'white'
          </span>
        </th>
        <td data-title="Function">
          <span>
            color('white')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-bg('white')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .bg-white
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</div>

### Spacing units
<div class="site-table-wrapper">
  <table class="usa-table--borderless site-table-responsive">
    <thead>
      <tr>
        <th scope="col" class="tablet:maxw-card-lg">Token</th>
        <th scope="col">Function</th>
        <th scope="col">Mixin</th>
        <th scope="col">Utility class</th>
      </tr>
    </thead>
    <tbody class="font-mono-2xs">
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            <a href="{{ site.baseurl }}/design-tokens/spacing-units/" class="token">units</a>
          </span>
        </th>
        <td data-title="Function">
          <span>
            units(<a href="{{ site.baseurl }}/design-tokens/spacing-units/" class="token">units</a>)
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-padding-x(<a href="{{ site.baseurl }}/design-tokens/spacing-units/" class="token">units</a>)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .padding-x-<a href="{{ site.baseurl }}/design-tokens/spacing-units/" class="token">units</a>
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            0.5<br/>
            <span class="display-inline-block padding-top-05">'05'</span>
          </span>
        </th>
        <td data-title="Function">
          <span>
            units(0.5)<br/>
            <span class="display-inline-block padding-top-05">units('05')</span>
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-padding-x(0.5)<br/>
            <span class="display-inline-block padding-top-05">u-padding-x('05')</span>
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .padding-x-05
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            1
          </span>
        </th>
        <td data-title="Function">
          <span>
            units(1)
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-border(1)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .border-1
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'card-lg'
          </span>
        </th>
        <td data-title="Function">
          <span>
            units('card-lg')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-width('card-lg')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .width-card-lg
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</div>

### Font size
<div class="site-table-wrapper">
  <table class="usa-table--borderless site-table-responsive">
    <thead>
      <tr>
        <th scope="col" class="tablet:maxw-card-lg">Token</th>
        <th scope="col">Function</th>
        <th scope="col">Mixin</th>
        <th scope="col">Utility class</th>
      </tr>
    </thead>
    <tbody class="font-mono-2xs">
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            <a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>,
            <a href="{{ site.baseurl }}/design-tokens/typesetting/font-size/" class="token">size</a>
          </span>
        </th>
        <td data-title="Function">
          <span>
            size(<a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>, <a href="{{ site.baseurl }}/design-tokens/typesetting/font-size/" class="token">size</a>)
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-size(<a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>, <a href="{{ site.baseurl }}/design-tokens/typesetting/font-size/" class="token">size</a>)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            —
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'sans', '3xs'
          </span>
        </th>
        <td data-title="Function">
          <span>
            size('sans', '3xs')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-size('sans', '3xs')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            —
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'ui', 'micro'
          </span>
        </th>
        <td data-title="Function">
          <span>
            size('ui', 'micro')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-size('ui', 'micro')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            —
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'body', 15
          </span>
        </th>
        <td data-title="Function">
          <span>
            size('body', 15)
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-size('body', 15)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            —
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</div>

### Font family
<div class="site-table-wrapper">
  <table class="usa-table--borderless site-table-responsive">
    <thead>
      <tr>
        <th scope="col" class="tablet:maxw-card-lg">Token</th>
        <th scope="col">Function</th>
        <th scope="col">Mixin</th>
        <th scope="col">Utility class</th>
      </tr>
    </thead>
    <tbody class="font-mono-2xs">
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            <a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>
          </span>
        </th>
        <td data-title="Function">
          <span>
            family(<a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>)
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-family(<a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-family-<a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'sans'
          </span>
        </th>
        <td data-title="Function">
          <span>
            family('sans')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-family('sans')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-family-sans
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'ui'
          </span>
        </th>
        <td data-title="Function">
          <span>
            family('ui')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-family('ui')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-family-ui
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'body'
          </span>
        </th>
        <td data-title="Function">
          <span>
            family('body')
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font-family('body')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-family-body
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</div>

### Font family and size together
<div class="site-table-wrapper">
  <table class="usa-table--borderless site-table-responsive">
    <thead>
      <tr>
        <th scope="col" class="tablet:maxw-card-lg">Token</th>
        <th scope="col">Function</th>
        <th scope="col">Mixin</th>
        <th scope="col">Utility class</th>
      </tr>
    </thead>
    <tbody class="font-mono-2xs">
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            <a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>,
            <a href="{{ site.baseurl }}/design-tokens/typesetting/font-size/" class="token">size</a>
          </span>
        </th>
        <td data-title="Function">
          <span>
            —
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font(<a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>, <a href="{{ site.baseurl }}/design-tokens/typesetting/font-size/" class="token">size</a>)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-<a href="{{ site.baseurl }}/design-tokens/typesetting/font-family" class="token">family</a>-<a href="{{ site.baseurl }}/design-tokens/typesetting/font-size/" class="token">size</a>
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'sans', '3xs'
          </span>
        </th>
        <td data-title="Function">
          <span>
            —
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font('sans', '3xs')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-sans-3xs
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'ui', 'micro'
          </span>
        </th>
        <td data-title="Function">
          <span>
            —
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font('ui', 'micro')
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-ui-micro
          </span>
        </td>
      </tr>
      <tr>
        <th scope="row" data-title="Token" class="tablet:text-no-wrap tablet:maxw-card-lg text-normal">
          <span>
            'body', 15
          </span>
        </th>
        <td data-title="Function">
          <span>
            —
          </span>
        </td>
        <td data-title="Mixin">
          <span>
            u-font('body', 15)
          </span>
        </td>
        <td data-title="Utility class">
          <span>
            .font-body-15
          </span>
        </td>
      </tr>
    </tbody>
  </table>
</div>
