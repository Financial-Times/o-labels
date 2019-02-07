
# o-labels [![Build Status](https://circleci.com/gh/Financial-Times/o-labels.png?style=shield&circle-token=baf3bd7fe9625dfc5c7e24a5451253b348cd9102)](https://circleci.com/gh/Financial-Times/o-labels) [![MIT licensed](https://img.shields.io/badge/license-MIT-blue.svg)](#licence)

Labels for content classification or to emphasise a value.

- [Usage](#usage)
  - [Markup](#markup)
  - [Sass](#sass)
- [Migration guide](#migration-guide)
- [Contact](#contact)
- [Licence](#licence)


## Usage

### Markup

The most minimal markup for a label is as follows:

```html
<span class="o-labels">Label</span>
```

Labels are displayed inline so including the above markup in a paragraph, for example, will make it sit alongside the text.

There are several size modifier classes which can be used to change the general appearance of a label:

```html
<span class="o-labels o-labels--big">Big Label</span>
<span class="o-labels o-labels--small">Small Label</span>
```

Labels can also have one of several states. The available states depend on which brand you are using (there are no states for whitelabel branded components):

#### Masterbrand

The following states are used to categorise content, mostly on FT.com:

```html
<span class="o-labels o-labels--content-commercial">Paid Post</span> (used for paid post and promoted content)
<span class="o-labels o-labels--content-premium">Premium</span> (used for premium-only content)
```

The following state is used to indicate that a feature is in a beta state:

```html
<span class="o-labels o-labels--lifecycle-beta">Beta</span>
```

#### Internal

The following states are used to represent the different support levels of Origami components:

```html
<span class="o-labels o-labels--support-active">Active</span>
<span class="o-labels o-labels--support-maintained">Maintained</span>
<span class="o-labels o-labels--support-experimental">Experimental</span>
<span class="o-labels o-labels--support-deprecated">Deprecated</span>
<span class="o-labels o-labels--support-dead">Dead</span>
```

The following states are used to represent the FT's service tiers:

```html
<span class="o-labels o-labels--support-platinum">Platinum</span>
<span class="o-labels o-labels--support-gold">Gold</span>
<span class="o-labels o-labels--support-silver">Silver</span>
<span class="o-labels o-labels--support-bronze">Bronze</span>
```

### Sass

#### Silent mode

As with all Origami components, o-labels has a [silent mode](http://origami.ft.com/docs/syntax/scss/#silent-styles). To use its compiled CSS (rather than incorporating its mixins into your own Sass) set `$o-labels-is-silent: false;` in your Sass before you import the o-labels Sass:

```sass
$o-labels-is-silent: false;
@import 'o-labels/main';
```

#### Mixin: `oLabels`

If using o-labels in silent mode, you'll need to use the mixins outlined here to output styles.

The `oLabels` mixin is used to output base styles as well as styles for _all_ of the label sizes and states. This output includes the `o-labels` classes:

```scss
@include oLabels();
```

```css
.o-labels {
    /* styles */
}
.o-labels--big {
    /* styles */
}
/* etc. */
```

If you wish to specify a subset of sizes and states to output styles for, you can pass in options (see [sizes](#sizes) and [states](#states) for available options):

```scss
@include oLabels($opts: (
    $sizes: ('big'),
    $states: (
        'content-commercial',
        'content-premium'
    )
));
```

#### Mixin: `oLabelsState`

The `oLabelsState` mixin can be used to output a class for one of the label states, outlined in the [states table](#states):

```scss
@include oLabelsState('content-commercial');
```

```css
.o-labels--content-commercial {
    /* styles */
}
```

The `oLabelsState` mixin also accepts optional custom configurations, which override defaults or allow you to define your own label states:

```scss
@include oLabelsState('citrus-fruit', (
    background-color: oColorsGetPaletteColor('lemon')
));
```

```css
.o-labels--citrus-fruit {
    /* styles */
}
```

#### Sizes

This table outlines all of the possible sizes you can request in the [`oLabels` mixin](#mixin-olabels):

| Size  | Description                                 | Brand support                |
|-------|---------------------------------------------|------------------------------|
| big   | Label with increased font size and padding. | master, internal, whitelabel |
| small | Label with decreased font size and padding. | master, internal, whitelabel |

#### States

This table outlines all of the possible states you can request in the [`oLabels` mixin](#mixin-olabels) and [`oLabelsState` mixin](#mixin-olabelsstate):

| Size                 | Description                                                   | Brand support |
|----------------------|---------------------------------------------------------------|---------------|
| content-commercial   | Used to identify paid posts or promoted content.              | master        |
| content-premium      | Used to identify premium content.                             | master        |
| lifecycle-beta       | Used to identify a feature that's in beta.                    | master        |
| support-active       | Used to indicate that a component is actively maintained.     | internal      |
| support-maintained   | Used to indicate that a component is maintained.              | internal      |
| support-experimental | Used to indicate that a component is an experimental feature. | internal      |
| support-deprecated   | Used to indicate that a component is deprecated.              | internal      |
| support-dead         | Used to indicate that a component is no longer worked on.     | internal      |
| tier-platinum        | Used to indicate a service with a platinum service tier.      | internal      |
| tier-gold            | Used to indicate a service with a gold service tier.          | internal      |
| tier-silver          | Used to indicate a service with a silver service tier.        | internal      |
| tier-bronze          | Used to indicate a service with a bronze service tier.        | internal      |


## Migration guide

### How to upgrade from v3.x.x to v4.x.x?

  - The `oLabels` mixin parameters have been changed, and all of the  mixins have changed significantly. See the [Sass documentation](#sass) for how to use the new and updated mixins
  - The following states have been removed. The decision to remove was based on a search of the various codebases using o-labels, if you need one of the removed states then please contact us and we'll add it back:
    - `active`: This state has been removed entirely
    - `brand`: This state has been removed entirely
    - `closed`: This state has been removed entirely
    - `error`: This state has been removed entirely
    - `live`: This state has been removed entirely
    - `pending`: This state has been removed entirely
    - `normal`: The normal state is achieved by not including a state modifier class
  - The following states have been renamed. This rename applies to both the default classes as well as the value passed into the `oLabelsState` mixin:
    - ```diff
      + content-commercial
      - commercial-content
      ```
    - ```diff
      + content-premium
      - premium
      ```
  - o-colors use-cases have been removed. If you wish to configure label colours we now recommend using the `oLabelsState` mixin and passing in variant config.

### How to upgrade from v2.x.x to v3.x.x?

V3 of o-labels removes the `oLabelsSize` mixin. To create different sized labels for your product you should use the o-typography mixins as shown in the [controlling label size](#controlling-label-size) section.

---


## Contact

If you have any questions or comments about this component, or need help using it, please either [raise an issue](https://github.com/Financial-Times/o-labels/issues), visit [#ft-origami](https://financialtimes.slack.com/messages/ft-origami/) or email [Origami Support](mailto:origami-support@ft.com).

---


## Licence

This software is published by the Financial Times under the [MIT licence](http://opensource.org/licenses/MIT).

