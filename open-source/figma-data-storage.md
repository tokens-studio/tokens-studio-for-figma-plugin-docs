---
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



Having a Token project that is over 100kb isn't a problem, it means you are doing great work! However, Figma's efforts to tackle their performance issues means Plugins like Tokens Studio need to implement special handling for larger token sets.



### Why is this happening?&#x20;

The Tokens Studio Plugin uses Figma's plugin API to interact with your design elements, styles and variables.&#x20;

As of May 2025, Figma is enforcing a limit on how much data a plugin can **store** in a Figma file via its `setSharedPluginData` API call.

> The total size of your entry (`namespace`, `key`, `value`) cannot exceed 100 kB. - [Figma Developer, Plugin API ](https://www.figma.com/plugin-docs/api/properties/nodes-setplugindata/)

This means, if you are using Local Document storage for your larger projects (small component libraries, lots of variables etc), you are likely to hit the 100kb data limit.&#x20;

{% hint style="info" %}
The data limit **does not apply** if you are syncing your Tokens to a remote storage provider as the Token project data is being stored outside of the Figma file.
{% endhint %}



### How it works

There is no action required by you! The plugin will work some magic under the hood to keep file sizes as small as possible.&#x20;

<details>

<summary>What's happening under the hood?</summary>

#### Compression and Chunking

To stay within Figma's 100KB per key limit, we compress and chunk the values and themes data when their size exceeds the limit.

This means:
* `values` become `values_chunk_0`, `values_chunk_1`, `values_chunk_2`, etc.
* `themes` become `themes_chunk_0`, `themes_chunk_1`, `themes_chunk_2`, etc.

Each chunk is compressed using UTF-16 compatible compression (via lz-string) before being stored.

The chunked data is stored using multiple `setSharedPluginData` calls with different keys for each chunk. When retrieving the data, the plugin:
* Reads all chunks using corresponding `getSharedPluginData` calls
* Reassembles the chunks in the correct order
* Decompresses the combined data to restore the original token information

This chunking approach allows the plugin to work with token projects larger than Figma's 100kb limit while maintaining compatibility with Figma's API constraints.

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



## Advanced: Working with Chunked Data

For plugin developers or those who need to access token data programmatically, this section explains how to work with the chunked data format.

### How to Read Chunked Data

The following code can be run in the Figma plugin dev console to retrieve token values:

<details>
<summary>Code for retrieving token values</summary>

```javascript
// For token values
let compressedValues = '';

const metaRaw = figma.root.getSharedPluginData("tokens", "values_meta");

try {
  const meta = JSON.parse(metaRaw || '{}');

  if (meta.type === 'chunked' && typeof meta.count === 'number') {
    const chunks = [];

    for (let i = 0; i < meta.count; i++) {
      const chunk = figma.root.getSharedPluginData("tokens", `values_chunk_${i}`);
      chunks.push(chunk);
    }

    compressedValues = chunks.join('');
  } else {
    // Default fallback if type is 'single' or meta is missing
    compressedValues = figma.root.getSharedPluginData("tokens", "values");
  }
} catch (e) {
  console.warn('Failed to parse values_meta:', e);
  compressedValues = figma.root.getSharedPluginData("tokens", "values");
}

console.log('Retrieved compressed values:', compressedValues.substring(0, 100) + '...');
```

</details>

<details>
<summary>Code for retrieving themes</summary>

```javascript
// For themes
let compressedThemes = '';

const metaRaw = figma.root.getSharedPluginData("tokens", "themes_meta");

try {
  const meta = JSON.parse(metaRaw || '{}');

  if (meta.type === 'chunked' && typeof meta.count === 'number') {
    const chunks = [];

    for (let i = 0; i < meta.count; i++) {
      const chunk = figma.root.getSharedPluginData("tokens", `themes_chunk_${i}`);
      chunks.push(chunk);
    }

    compressedThemes = chunks.join('');
  } else {
    // Default fallback if type is 'single' or meta is missing
    compressedThemes = figma.root.getSharedPluginData("tokens", "themes");
  }
} catch (e) {
  console.warn('Failed to parse themes_meta:', e);
  compressedThemes = figma.root.getSharedPluginData("tokens", "themes");
}

console.log('Retrieved compressed themes:', compressedThemes.substring(0, 100) + '...');
```

</details>

### How to Decompress and View Your Data

{% hint style="warning" %}
This cannot be run in the Figma plugin Dev Console, as it does not support module imports or external libraries.
{% endhint %}

To decompress and view the chunked/compressed data (values or themes), you will need to do this in your own local development environment, such as a Node.js project, plugin codebase, or a browser-based tool with module support.

<details>
<summary>Steps to decompress data</summary>

1. Install lz-string:
```bash
npm install lz-string
```

2. Use the following code to decompress:
```javascript
import { decompressFromUTF16 } from "lz-string";

const jsonString = decompressFromUTF16(compressedValues); // or compressedThemes
const tokens = JSON.parse(jsonString);
console.log(tokens);
```

</details>

### How to Clear Shared Plugin Data (Including Chunks)

If you need to clear all token data from a Figma file, you can run this code in the dev console:

<details>
<summary>Code to clear all token data</summary>

```javascript
const keys = figma.root.getSharedPluginDataKeys("tokens");
const keysToDelete = keys.filter(k => 
  k === "values" || 
  k === "themes" || 
  k.startsWith("values_") || 
  k.startsWith("themes_")
);

keysToDelete.forEach(key => {
  figma.root.setSharedPluginData("tokens", key, "");
});

console.log(`Cleared ${keysToDelete.length} token data keys`);
```

</details>



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
