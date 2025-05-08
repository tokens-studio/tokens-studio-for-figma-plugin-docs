---
hidden: true
icon: square-info
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

# Figma Data Limits

## Figma Data Limits&#x20;

You may have noticed the size of your Token project is showing in the footer of the plugin.&#x20;

This can happen when you:

* Import a large volume of Styles or Variables from Figma.
* Upload a Token project into Tokens Studio from a JSON file or folder.
* Expand an existing Token project to have more Token Sets or Themes.&#x20;



As soon as the Plugin detects the project size is at 100kb and set to Local Document storage:

* The footer of the Plugin will display your current file size.&#x20;
* You can select the file size to open a modal with easy access to more information.&#x20;



Having a Token project that is over 100kb isn't a problem, it means you are doing great work! However, Figma's efforts to tackle their performance issues means Plugins like Tokens Studio&#x20;



### Why is this happening?&#x20;

The Tokens Studio Plugin uses Figma's plugin API to to interact with your design elements, styles and variables.&#x20;

As of May 2025, Figma is enforcing a limit on how much data a plugin can **store** in a Figma file via its `setSharedPluginData` API call.

> The total size of your entry (`namespace`, `key`, `value`) cannot exceed 100 kB. - [Figma Developer, Plugin API ](https://www.figma.com/plugin-docs/api/properties/nodes-setplugindata/)

This means, if you are using Local Document storage for your larger projects (small component libraries, lots of variables etc), you are likely to hit the 100kb data limit.&#x20;

{% hint style="info" %}
The data limit **does not apply** if you are syncing your Tokens to a remote storage provider as the Token project data is being stored outside of the Figma file.
{% endhint %}



### How it works

There is no action required by you! The plugin will work some magic under the hood to keep file sizes as small as possible.&#x20;

<details>

<summary>Whats happening under the hood?</summary>

When the Plugin detects the project size is at 100kb and set to Local Document storage, it will:

* Compress the data and break it into chunks smaller than 95kb when writing to Figma
* Combine the chunks and decompress when reading from Figma.&#x20;



When the Plugin is storing Token data remotely and you close the Plugin before you have pushed changes to your sync provider, the Plugin will:

* Store the changes you haven't pushed using a different API `figma.clientStorage` which stores it locally to your machine.&#x20;
* Client storage still has a data limit, but it is much larger (5mb).&#x20;

</details>

However, this process takes time! You will notice the Plugin starts to perform tasks slower as your file size increases.&#x20;

{% hint style="info" %}
The best way to avoid slowdowns in your workflow is to store your Tokens remotely using one of our integrated sync providers.
{% endhint %}



### Sync Tokens to remote storage to avoid issues&#x20;

Figma's 100kb data limit only applies when a plugin has to store (or save) information locally to the Figma File.&#x20;

This means, if you switch to a remote storage provider, the data limit does not apply and the plugin does not perform the extra steps listed above, giving you optimal performance in your Figma file.&#x20;



### Remote storage guides

If you haven't set up a remote sync provider yet, don't worry! These guides will walk you through it.&#x20;

{% hint style="info" %}
If you don't know which sync provider to use, try Github as a free option.&#x20;
{% endhint %}

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Add a new sync provider</strong> to start storing your tokens remotely. </td><td><a href="../../.gitbook/assets/cardHeader-sync-remote-manage.png">cardHeader-sync-remote-manage.png</a></td><td><a href="../manage-sync-provider/">manage-sync-provider</a></td></tr><tr><td><strong>Switch from local to remote storage</strong> if you already have a sync provider set up.</td><td><a href="../../.gitbook/assets/cardHeader-sync-remote-change.png">cardHeader-sync-remote-change.png</a></td><td><a href="../manage-sync-provider/change.md">change.md</a></td></tr><tr><td>See <strong>all the remote Token storage providers</strong> that Tokens Studio is integrated with. </td><td><a href="../../.gitbook/assets/cardHeader-sync-remote-overview.png">cardHeader-sync-remote-overview.png</a></td><td><a href="../remote/">remote</a></td></tr></tbody></table>



***



### Resources

Figma API Documentation Mentioned:

* Figma Developer - [Plugin API setPluginData](https://www.figma.com/plugin-docs/api/properties/nodes-setplugindata/)
* Figma Developer - [Plugin API figma.clientStorage](https://www.figma.com/plugin-docs/api/figma-clientStorage/)

#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Sync Local Storage](https://github.com/tokens-studio/figma-plugin/labels/sync%20local%20storage)

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* None yet

{% include "../../.gitbook/includes/featurebase.md" %}
