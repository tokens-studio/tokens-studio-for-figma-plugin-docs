---
icon: moon
cover: ../.gitbook/assets/pageHeader-themes-tsOnly.png
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

# Themes (pro)

## Themes (pro)

In software and web development, a Theme defines the styling choices applied to the graphic elements of an interface, influencing the appearance and atmosphere of websites and software applications within a specific context, such as a brand, platform, or user preference.&#x20;

When you are working with Design Tokens, the concept of theming enables you to style the same components in different ways so you can do more without needing to manage more components.

For example, instead of having 2 button components, light-mode button and dark-mode button, you have a single button component that takes on the styling properties of the color mode theme that is currently active.&#x20;



The Themes feature in Tokens Studio allow you to define combinations of Token Sets that are intended to be applied together to style design elements. Under the hood, the Plugin creates a themes configuration file that can be shared with developers and used in code.&#x20;

Multiple Themes can be applied at the same time to create a matrix of possible concepts that a single design element can be styled with. This is also known as _multi-dimensional theming_.&#x20;



### Themes Guides&#x20;

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Themes that switch - a simple example. </td><td><a href="../.gitbook/assets/cardHeader-themes-switch.png">cardHeader-themes-switch.png</a></td><td><a href="simple-switch-guide.md">simple-switch-guide.md</a></td></tr><tr><td>Export to Figma Styles and Variables using Themes. </td><td><a href="../.gitbook/assets/card-header-figma-export-themes.png">card-header-figma-export-themes.png</a></td><td><a href="../figma/export/themes.md">themes.md</a></td></tr></tbody></table>



We are working on several new guides to help you master working with Themes in the Tokens Studio Plugin for Figma - coming soon!&#x20;

* Creating, editing, and removing themes.&#x20;
* Multi-dimensional theming.&#x20;
* Detach styles and variables from Themes.&#x20;
* Attach local styles and variables to Themes.&#x20;







***



### Transforming Themes for use in Code

As soon as your Token project includes Themes, there are JSON files created by the plugin to save your configuration data so it can be shared with developers. Once developers have the new Themes files in your external storage provider, they can use that data in their transformation process to turn the themes file into usable code.&#x20;

{% include "../.gitbook/includes/transform-tokens-default-message.md" %}

SD-Transforms generic package includes a specific transforms to convert Tokens Studio themes into individual theme files for all possible permutations

→ [SD-Transforms Read-Me Doc, Theming](https://github.com/tokens-studio/sd-transforms?tab=readme-ov-file#theming)



#### Plugin Sync Settings

If this is the first time you are working with Themes in your project, theres a couple things you'll want to do in the Plugin Settings make the transformation process as simple as possible:&#x20;

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td>Sync to a remote storage provider, like GitHub, GitLab, Bitbucket or Azure DevOps.</td><td><a href="../.gitbook/assets/cardHeader-sync-remote-overview.png">cardHeader-sync-remote-overview.png</a></td><td><a href="../token-storage/remote/">remote</a></td></tr><tr><td>Configure your sync settings to save to a folder in your repository with multiple files. </td><td><a href="../.gitbook/assets/cardHeader-sync-remote-multi-file.png">cardHeader-sync-remote-multi-file.png</a></td><td><a href="../token-storage/remote-multi-file-sync.md">remote-multi-file-sync.md</a></td></tr></tbody></table>

***



### Resources

Mentioned in this Guide

* SD-Transforms Read-Me - [Theming](https://github.com/tokens-studio/sd-transforms?tab=readme-ov-file#theming)



Community resources:

* None yet!

{% include "../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Themes](https://github.com/tokens-studio/figma-plugin/labels/themes)

{% include "../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* None

{% include "../.gitbook/includes/featurebase.md" %}



