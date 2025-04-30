---
icon: webhook
cover: ../../../.gitbook/assets/pageHeader-token-type-typography-fontFallback.png
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

# Font Fallbacks

## Font Fallbacks

Font fallbacks are a common practice in code to ensure the text remains readable even when the primary font is unavailable.

> "A fallback font is a font face that is used when the primary font face is not loaded yet, or is missing [glyphs](https://fonts.google.com/knowledge/glossary/glyph) necessary to render page content. For example, the CSS below indicates that the `sans-serif` font family should be used as the font fallback for `Roboto`" - [Chrome for Developers](https://developer.chrome.com/blog/font-fallbacks#background)

While Figma doesn't natively support font fallbacks, Tokens Studio allows you to define fallbacks for **Font Family** and **Font Weight** Token Types.

***

### In the plugin

To define a fallback using the plugin, you can write the Token's value using the no-code or interface or modify the JSON file with comma-separated values.

#### Font Family Tokens

To implement font fallbacks in your Font Family Token:

* Use a comma-separated list in your token value.
* Write the Font name (string value) in order of preference, from primary to fallback options.
  * Be sure to follow the guidelines for best practices outlined in the Font Family Token documentation. #add-doc-link/typography
* Figma will use the first Font Family in the list.

Example:

```json
{
  "sans-serif": {
    "$value": "Arial, Helvetica",
    "$type": "fontFamilies"
  }
}
```



#### Typography Composite Tokens

When using Typography Composite Tokens, you can reference a Font Family Token that includes fallbacks:

```json
{
  "body-text": {
    "value": {
      "fontFamily": "{sans-serif}",
      "fontSize": "16px",
      "fontWeight": "400"
    },
    "type": "typography"
  }
}
```



***



### Limitations and Considerations

Figma will only display the primary font, not the fallbacks.

* When exporting to Figma variables or styles, only the primary font will be used.
* Fallbacks are primarily for web and application development, not for use within Figma itself.

While it might be tempting to use fallbacks as a way to work around Figma's nuanced way of Font Weight + Style values as a combined string, which is written differently for each Font Family, we don't recommend this approach.

* We will always pass the first value to Figma, so if it doesn't match, you'll still get the error even if you included the correct value as a fallback.
* Tokens are intended to be used in code, which isn't as particular as Figma. So when you engineers receive a Font Weight Token with the same value repeated multiple times it might lead to unexpected results.

***

### Transforming Tokens

{% include "../../../.gitbook/includes/transform-tokens-default-message.md" %}

When transforming tokens for use in code, the Style Dictionary handles font fallbacks appropriately:

* `fontFamily` Tokens that contain multiple values (comma separated) will be processed slightly for CSS to ensure that when a Font Family name contains spaces, the value is put in quotes `'` so it works in CSS.

→ Style Dictionary - [Built in Transforms fontFamily/CSS](https://v4.styledictionary.com/reference/hooks/transforms/predefined/#fontfamilycss)



***



### Resources

Mentioned in this doc:

* SD-Transforms - [Read Me](https://github.com/tokens-studio/sd-transforms#readme)
* Style Dictionary - [https://styledictionary.com/](https://styledictionary.com/)

#### CSS resources:

* Chrome Developer Docs - [Improved Fallback Fonts](https://developer.chrome.com/blog/font-fallbacks#background)
* MDN Web Docs - [font-family](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family)
* CSS-Tricks - [CSS Basics: Fallback Font Stacks for More Robust Web Typography](https://css-tricks.com/css-basics-fallback-font-stacks-robust-web-typography/)

#### Community resources:

* None yet!

{% include "../../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - Tokens Studio Plugin GitHub - [Open issues for Token Type Font Family](https://github.com/tokens-studio/figma-plugin/labels/token%20type%20font%20family)

{% include "../../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* None

{% include "../../../.gitbook/includes/featurebase.md" %}
