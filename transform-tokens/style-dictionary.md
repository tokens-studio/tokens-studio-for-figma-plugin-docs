---
icon: npm
layout:
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

# Style Dictionary + SD Transforms

## Transforming Design Tokens with Style Dictionary

[Style Dictionary](https://styledictionary.com/) is a powerful tool for transforming design tokens into usable code for different platforms, such as the web with CSS variables.&#x20;

Tokens coming from Tokens Studio require an additional step: [@Tokens-studio/sd-transforms](https://www.npmjs.com/package/@tokens-studio/sd-transforms), an npm package that prepares Tokens for Style Dictionary.

This guide covers the basics of installing and using Style Dictionary. For full details, head to [https://styledictionary.com/](https://styledictionary.com/)&#x20;



### Install with NPM

Before we begin, we need to install Style Dictionary. You can install it using npm, which is a package manager for Node.js. Open your terminal and run the following command:

```
npm install style-dictionary
```



### Using Style Dictionary

Once Style Dictionary is installed, we can start transforming our design tokens. Here's an overview of the process:

1. Define your design tokens in a JSON file.
2. Configure Style Dictionary to transform your design tokens into usable code.
3. Generate code for your target platform.



### SD-Transforms

We provide official transforms in the form of a package called [@tokens-studio/sd-transforms](https://www.npmjs.com/package/@tokens-studio/sd-transforms). You can customize these transforms or create your own to fit your needs. More information can be found on npm.



### Style Dictionary Configurator

[Style Dictionary Configurator](https://configurator.tokens.studio/) is a web-based tool that allows you to transform your design tokens directly in your browser. It uses Style Dictionary under the hood and can be a convenient way to experiment with Style Dictionary without installing it on your computer.

{% include "../.gitbook/includes/spacer-image-fullwidth.md" %}
