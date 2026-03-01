---
icon: code-pull-request
---

# Contribute

## Contributing

If you want to get started contributing to Tokens Studio for Figma, here's how you can get started:

1. Run `yarn  --frozen-lockfile  --immutable` to install dependencies.
2. Run `yarn start` to start webpack in watch mode or `yarn build` to build once.
3. Open `Figma` -> `Plugins` -> `Development` -> `Import plugin from manifest...` and select the `manifest.json` file from the relevant package.
4. Create a pull request for your branch, including as much information as possible within the provided template.


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
