---
icon: code-pull-request
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

# Contribute

## Contributing

If you want to get started contributing to Tokens Studio for Figma, here's how you can get started:

1. Run `npm ci` to install dependencies.
2. Run `npm run start` to start webpack in watch mode or npm run build to build once.
3. Open Figma -> Plugins -> Development -> New Plugin... and choose manifest.json file from this repo.
4. Create a Pull request for your branch



### Known Issues

You may run into some common errors, listed below.



#### **Cannot read property document of undefined**

This error can be solved by clearing Figma's cache. To do that follow the steps outlined in [this document](https://help.figma.com/hc/en-us/articles/360040328553-Can-I-work-offline-with-Figma-#clear-data).

```
Mac
Use the Terminal app to clear the cache.

Quit the Figma desktop app.
Open the Terminal.app and enter the following command:  rm -rf "$HOME/Library/Application Support/Figma/"{Desktop,DesktopProfile}
Try opening the Figma desktop app again.
```

{% include "../.gitbook/includes/spacer-image-fullwidth.md" %}
