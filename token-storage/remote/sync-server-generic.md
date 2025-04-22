---
icon: box-taped
cover: ../../.gitbook/assets/GENERICVERSION-page-header-sync-provider.png
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

# Generic Versioned Storage - Server Sync Provider

## Generic Versioned sync setup guide

For projects requiring highly controlled and secure data-sharing environments, you can host your Design Token JSON files on your servers or storage solutions.

You can use the Tokens Studio plugin to keep your Design Tokens in sync with your code files _**without**_ passing your design data through any Git or 3rd-party storage providers.

We support two-way sync, meaning you can use the plugin to:

* **push** JSON files of Design Tokens to your storage provider
* **pull** the Tokens stored in your storage provider into any Figma file

You can configure the permissions of your Generic Versioned sync to be:

* Read Only
* Read / Write
* Read / Write / Create

This means the Design Tokens living in code are the source of truth for our design decisions, which can be shared between design and development teams.

This doc outlines how to configure Generic Versioned storage and add it as a **Sync provider** in the plugin.

### How it works

* Once your Token JSON files are **stored on your server**, capture the **URL endpoint**.
* **Configure a new Generic Versioned sync provider** within the plugin.
* Use the plugin to **sync Design Token changes** between your server and Figma design files.

***

### Generic Versioned sync setup instructions

If you haven't already, store your Design Token JSON files on your server and create a storage endpoint.

→ [Here's an example implementation of token JSON files stored on a SQLite database on a local file if you need a reference.](https://github.com/SorsOps/figma-tokens-generic-storage-example)

* [The swagger is available with the necessary schemas to roll your own endpoint.](https://github.com/SorsOps/figma-tokens-generic-storage-example/blob/main/public/swagger.json)

→ [Here's a guide on using a JSON server as a simple way to use Generic Versioned storage created by Ian Lawton, a Tokens Studio Community member.](https://medium.com/@ian.lawton/a-simple-design-token-storage-server-for-figma-token-studio-3a9ba74aefb5)



#### 1. Storage URL

**Copy the URL** where your Token JSON files are stored.

* **Store it somewhere safe**, as it's needed for the plugin configuration.



#### 2. Capture header pairs

Headers are optional authentication instructions for the plugin set up as **key value pairs**.

* Refer to your server technical documentation for more details on headers.

For example, if you want to identify and track which users are accessing your Token files, you could set up a **user authorization** header:

* Name = `Authorization`
* Value = `username`

If your server requires authentication:

* **Copy and save the required header pair** somewhere safe, as it's needed for the plugin configuration.

***

### Configuring Tokens Studio Plugin

In Figma, open the Tokens Studio plugin and navigate to the **Settings** page.

* Under the **Sync providers** section, select the **Add new** button to see a list of all Token storage providers.
* Select **Generic Versioned**

<figure><img src="../../.gitbook/assets/settings-page-genericversion-v2-0.png" alt=""><figcaption></figcaption></figure>

#### Add credentials for Generic Versioned sync

You'll need the information saved from the steps above to complete the Tokens Studio sync configuration form.

<figure><img src="../../.gitbook/assets/sync-generic-annotated-v2-0.png" alt=""><figcaption></figcaption></figure>



**1. Name**

This is a **nickname** that appears in the plugin settings page later on to identify this specific sync provider configuration.

* Choose something memorable to you and your project.
* Example: `Hyma brand exploration`



**2. URL**

Enter the complete **URL** you saved from [step 1 above.](sync-server-generic.md#id-1.-storage-url)



**3. Flow type (permissions)**

The flow type sets the permissions between the plugin and your storage provider.

* **Read Only**
  * Token data is pulled into the plugin to be viewed but cannot be edited.
    * Read requests are sent via **GET** calls to the endpoint.
* **Read / Write**
  * Token data is pulled into the plugin to be viewed, and edits to those Tokens can be made and pushed back to storage.
  * New Tokens, sets, or themes can not be created.
    * Read/Write requests are sent via **PUT** requests to the endpoint.
* **Read / Write / Create**
  * New Tokens, sets, and themes can be created.
  * Token data can be pushed and pulled between the plugin and your storage provider for two-way sync.
    * Read/Write/Create requests are sent via **POST** requests to the endpoint.
    * The **POST** request is expected to return:
      * Validation that the endpoint has tracking setup (or not)
      * `updatedAt` field in the JSON, which can be used to set additional workflows on the storage side, like additional **GET** requests.



**4. Headers**

The optional authentication **headers** you saved from [step 2 above](sync-server-generic.md#id-2.-capture-header-pairs).



#### Save and do the initial sync

Save to confirm your credentials, and follow the prompts in the plugin to finish setting up the sync to your Generic Versioned provider.

{% include "../../.gitbook/includes/add-new-sync-provider.md" %}

***

### Shared source of truth

As you work in the plugin, push and pull indicators remind you to stay in sync.

{% include "../../.gitbook/includes/push-pull.md" %}

Once your Token JSON files are synced to your external storage, you have a shared source of truth between Designers and Engineers!

{% include "../../.gitbook/includes/transforming-tokens.md" %}



***

### Resources

Mentioned in this doc:

* GitHub - [Generic Versioned Example Repo from Tokens Studio](https://github.com/SorsOps/figma-tokens-generic-storage-example)
  * [Swagger example to roll your own endpoint.](https://github.com/SorsOps/figma-tokens-generic-storage-example/blob/main/public/swagger.json)
* SD-Transforms - [Read Me](https://github.com/tokens-studio/sd-transforms#readme)
* Style Dictionary - [https://styledictionary.com/](https://styledictionary.com/)



Community resources:

* Ian Lawson's Guide (Medium Article) - [A simple Design Token storage server for Figma Tokens Studio](https://medium.com/@ian.lawton/a-simple-design-token-storage-server-for-figma-token-studio-3a9ba74aefb5)

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for URL sync](https://github.com/tokens-studio/figma-plugin/labels/sync%20url)

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* 🧑‍💻 [Sync to external token storage enhancements - Feature Request](https://tokensstudio.featurebase.app/p/sync-external-storage-enhancements)
  * How might we improve the experience of working with sync providers in general?
* ↕️ [Git sync enhancements - push, pull, merge, branching - Feature Request](https://feedback.tokens.studio/p/git-sync-enhancements)
* 🔐 [Data security info request - Feature Request](https://feedback.tokens.studio/p/data-security-info)

{% include "../../.gitbook/includes/featurebase.md" %}
