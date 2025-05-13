---
icon: figma
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

# Shared Plugin Data

## Shared Plugin Data

We believe data stored by the Tokens Studio Plugin should be accessible by other Figma plugin makers as well, to create a thriving ecosystem of tools all being able to communicate with one another.&#x20;

Imagine a world where we're able to store plugin data on a layer or document, and other plugins can pick that back up, and do the things their plugin does best. This is why we've opened up the plugin data that the plugin stores on your document or nodes so you can use it with other plugins as well.



### How it works

We're storing tokens stored on a document on the shared plugin data namespace `tokens`. Other plugins can read from that. Also, we're storing applied decisions on each node on the same shared namespace. All you'd need to do is find out what tokens are stored on a node. Figma provides a couple of helpful functions to do so.


### Compression and Chunking

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


### Advanced: Working with Chunked Data

For plugin developers or those who need to access token data programmatically, this section explains how to work with the chunked data format.

#### How to Read Chunked Data

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

```

</details>

#### How to Decompress and View Your Data

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

#### How to Clear Shared Plugin Data (Including Chunks)

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


#### Getting tokens applied on a layer

`node.getSharedPluginData("tokens", key)` gives you the token that was applied on that `node` for that `key`.&#x20;

To find out what `keys` are available, you'd first run `node.getSharedPluginDataKeys("tokens")` on the `node` to find out what `keys` are set.&#x20;

With that result you're able to query the stored tokens.



#### Apply Tokens on a layer

`node.setSharedPluginData("tokens", key, value)` allows you to store a token on a layer. You'd need to make sure that `key` is [any of the plugin data keys](https://github.com/tokens-studio/figma-plugin/blob/main/src/config/properties.js) that we're using.



### Figma Plugin Helpers

We've [built a tool](https://www.npmjs.com/package/@six7/figma-tokens-helpers) that allows you to read all of the above more easily in your own plugin. We're exposing functions that wrap our plugin data functions, so you can easily get tokens stored on the document, on the layer, and even get the resolved tokens taking the activated sets/themes into account!



{% include "../.gitbook/includes/spacer-image-fullwidth.md" %}
