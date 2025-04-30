---
icon: function
cover: ../../.gitbook/assets/pageHeader-tokenValue-Math.png
coverY: 0
layout:
  cover:
    visible: true
    size: full
  title:
    visible: false
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Using Math in Token Values

## Using Math in Token Values

Tokens Studio supports math equations to calculate the Value of a Token.

This is a popular approach to a create scales for typography, spacing, size, or dynamically calculate the radius of a focus ring (pictured above).

Combining math equations with referenced to another Token can create a flexible and powerful design system.&#x20;



### Token Types compatible with math

All Token Types that accept numeric values can use math equations to calculate their value in Tokens Studio.&#x20;

When you apply a Token with a math equation as its value, the Plugin applies the resolved value to the corresponding property in Figma.&#x20;

_Select a card to jump to its technical docs._&#x20;

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Dimension</td><td><a href="../../.gitbook/assets/card-header-token-type-dimension.png">card-header-token-type-dimension.png</a></td><td><a href="../token-types/dimension/">dimension</a></td></tr><tr><td>Number</td><td><a href="../../.gitbook/assets/card-header-token-type-number.png">card-header-token-type-number.png</a></td><td><a href="../token-types/number.md">number.md</a></td></tr><tr><td>Spacing</td><td><a href="../../.gitbook/assets/card-header-token-type-spacing.png">card-header-token-type-spacing.png</a></td><td><a href="../token-types/dimension/spacing.md">spacing.md</a></td></tr><tr><td>Sizing</td><td><a href="../../.gitbook/assets/card-header-token-type-sizing.png">card-header-token-type-sizing.png</a></td><td><a href="../token-types/dimension/sizing.md">sizing.md</a></td></tr><tr><td>Border Width</td><td><a href="../../.gitbook/assets/card-header-token-type-borderwidth.png">card-header-token-type-borderwidth.png</a></td><td><a href="../token-types/dimension/border-width.md">border-width.md</a></td></tr><tr><td>Border Radius</td><td><a href="../../.gitbook/assets/card-header-token-type-border-radius.png">card-header-token-type-border-radius.png</a></td><td><a href="../token-types/dimension/border-radius.md">border-radius.md</a></td></tr><tr><td>Font Size</td><td><a href="../../.gitbook/assets/card-header-token-type-font-size.png">card-header-token-type-font-size.png</a></td><td><a href="../token-types/typography/font-size.md">font-size.md</a></td></tr><tr><td>Line Height</td><td><a href="../../.gitbook/assets/card-header-token-type-line-height.png">card-header-token-type-line-height.png</a></td><td><a href="../token-types/typography/line-height.md">line-height.md</a></td></tr><tr><td>Letter Spacing</td><td><a href="../../.gitbook/assets/card-header-token-type-letter-spacing.png">card-header-token-type-letter-spacing.png</a></td><td><a href="../token-types/typography/letter-spacing.md">letter-spacing.md</a></td></tr></tbody></table>



{% hint style="info" %}
Number variables in Figma doesn't support Math equations
{% endhint %}

This means when you export a Token with math in its value as a Variable in Figma:

* You won't see the references or equations.
* The plugin sends the resolved value of the equation to Figma as a Number Variable.

***



### Possible Values

Token Values written as equations can include hard-coded number values and references to other Tokens.&#x20;



For example, if you want `spacing.lg` to be twice as large as `spacing.md` you can write an equation to calculate its value:

```
{spacing.md} * 2
```



Or, you can replace the multipler with a reference to another Token named `scale.multiplier`&#x20;

```
{spacing.md} * {spacing.multipler}
```



#### Syntax

The syntax for writing a math equation varies based on the kind of equation you are writing.



Simple math equations can be written with or without brackets.&#x20;

For example, `8 * 8` and `(8 * 8)` will both resolve to `64`



Complex formulas require spaces between operators to ensure the Tokens can be transformed correctly using Style Dictionary.&#x20;

For example: `8 * 8` will transform as expected `8*8` will not.&#x20;

{% hint style="info" %}
Looking for more complex formulas supported in the Plugin?&#x20;

Here's the docs for [the math package used](https://www.npmjs.com/package/expr-eval?activeTab=readme) under the hood.
{% endhint %}

***



### Known limitations

Working with math in the plugin can be a powerful workflow enhancement, but there are some limitations to be aware of.

#### Multi-value Tokens won't resolve

The plugin supports Tokens with more than one value. When these Tokens are referenced in a math equation, the plugin can not resolve the equation because it doesn't know how to interpret the value.

For example, a [Spacing Token](../token-types/dimension/spacing.md#multiple-values) with `2,4` as its value represents spacing on top/bottom and right/left.



#### Units in equations

Referencing Tokens in our math equations that have values that contain units can lead to unexpected results.

This is because the math package we use can resolve equations with units, as long as the units aren't mixed.

For example:

* A Token named `size-2` with a value of `1.5rem`
* A Token named `density-default` with a value of `2px`

When both Tokens are included in a math equation written as:

```
{size-2} + {density-default}
```

The equation can't be resolved because the Tokens referenced contain a mix of `rem` and `pixel` units. If both Tokens have the same units, or are unitless, the equation would resolve as expected.



**Workarounds**

One method is to create your math equations using the [Other](../token-types/other.md) or [Number Token](../token-types/number.md) Types which don't require a unit, and add them in later.

For example, you could create a sizing scale using then add the required unit when it is referenced in a [Typography Token](../token-types/typography/).

* lineHeights = `{lineHeights-calc-body-default}%`
* fontSize = `{scale-rem-md}rem`

***



### Equations to try

Here are some math equations used by our team.

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Round to the nearest whole number

When using multipliers that aren't a whole number, you can use a rounding function to calculate values that don't include decimals, because a spacing value of `12.11px` might not be ideal.

To round to the nearest whole number, you can put our equation inside the `roundTo` function.

For example, if `sizing.sm` has a value of `2`

```
roundTo({sizing.sm} * 1.33, 0)
```

`2 * 1.33 = 2.66`

Will calculate a resolved value of  `3`



#### Create a percentage from a unitless number

In Figma, the only option for a [responsive line-height value is in percentage](../token-types/typography/line-height.md), but your engineers might prefer the Token defined as a unitless number.

In this case, you can create a unitless Number Token with the preferred value, and write an equation in the [Typography Composite Token](../token-types/typography/#possible-values) to convert it to a percentage so it works well with Figma.&#x20;

For example, the Number Token called `lineHeights-unitless.heading.relaxed` with a value of `1.5` would be written in a Line Height Token as:

```
{lineHeights-unitless.heading.relaxed} * 100%
```

Which calculates a resolved value of `150%`



#### Convert unitless numbers to rem

This equation requires having a Token which defines the value of 1 rem, and adjusting the Tokens Studio plugin settings to reference this Token as the value for "base font size".

[_→ Jump to the guide on Base Font Size Settings_](../../manage-settings/base-font-size.md)

In this example, there is a&#x20;

* Number Token called `unitless-Token` with a value of `48`
* Number Token called `rem-base` with a value of `16`

A new Dimension Token is created with the value as an equation:

```
{unitless-Token} / {rem-base} * 1rem
```

Which calculates a resolved value of `3rem`

***



### W3C DTCG Token Format

At the time of writing this doc, Math as a Token value is not mentioned in [the most recent Design Tokens Community Group W3C specifications](https://tr.designtokens.org/format/) for Design Tokens.

Tokens Studio has included this feature in the plugin to help design system maintainers work more efficiently.

***



### Transforming Tokens

{% include "../../.gitbook/includes/transform-tokens-default-message.md" %}

When transforming Tokens with Math in their Values, there are specific configurations to be aware of.



Token Values entered with math equations need to be checked and resolved.

→ [SD-Transforms Read-Me Doc, ts/resolveMath](https://github.com/tokens-studio/sd-transforms/?tab=readme-ov-file#tssizepx)



Token Values entered as a number without a unit converted to a number with pixels as a unit.

→ [SD-Transforms Read-Me Doc, ts/size/px](https://github.com/Tokens-studio/sd-transforms/?tab=readme-ov-file#tssizepx)

{% hint style="info" %}
Having trouble with Math equations not resolving properly? Check your syntax! \
[↑ Spaces are required between operators as described above. ](math.md#syntax)
{% endhint %}

***



### Resources

Tokens Studio uses the JavaScript Expression Evaluator for the implementation of math in token values.

* nmp - [JavaScript Expression Evaluator](https://www.npmjs.com/package/expr-eval?activeTab=readme)



Mentioned in this doc:

* SD-Transforms - [Read Me](https://github.com/tokens-studio/sd-transforms)
* Style Dictionary - [Read Me](https://amzn.github.io/style-dictionary/#/)
* Design Tokens Community Group - [W3C Draft](https://tr.designtokens.org/format/)



#### Community resources:

* Sam I am Designs has a written guide and Figma community file featuring many of the math equations mentioned above.
  * [Sam's Fancy Math Equations in Tokens Studio](https://samiamdesigns.substack.com/p/sams-fancy-math-equations-in-tokens)

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Token Values Math](https://github.com/tokens-studio/figma-plugin/labels/token%20value%20-%20math%20functions)

* None yet

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* Math in token value enhancements - [Feature Request](https://feedback.tokens.studio/p/math-in-value-enhancements)

{% include "../../.gitbook/includes/featurebase.md" %}
