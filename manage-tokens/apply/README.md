---
hidden: true
icon: circle-plus
cover: ../../.gitbook/assets/PAGEheader-figma-applyToken.png
coverY: 0
---

# Apply Tokens to Figma elements

## Apply Tokens to Figma design elements

Whenever you left-click a token in the plugin and have a layer selected in Figma, we will apply that tokens value to the layer. That could mean for a rectangle, we apply a color token as a fill, or a border radius as the radius.

You can also right-click each token in the plugin to choose from available properties to apply to. What happens in the background is that we will apply a "shared plugin data" to Figma's underlying plugin API, binding that layer to that token name.

