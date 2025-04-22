---
icon: file
cover: ../.gitbook/assets/LOCAL-page-header-sync-provider.png
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

# Local Document - Figma File Token Storage

## Local Figma Document Token Storage

By default, Tokens Studio will store your Design Tokens locally in the Figma file you are working in.

This limits your ability to share your Tokens across multiple Figma files. A **sync provider** is required for a [multi-file workflow in Figma](../figma/non-local-files.md).

{% content-ref url="remote/" %}
[remote](remote/)
{% endcontent-ref %}

Once you have added one or more Sync Providers to Tokens Studio, you can temporarily store your tokens locally in the Figma file. This is helpful for offline work, saving backups of your Figma files, or prepping a file to share with other people who won't have access to your sync provider.

<figure><img src="../.gitbook/assets/settings-page-sync-localOnly-v2-01 (1).png" alt=""><figcaption></figcaption></figure>

### Steps in the plugin for Figma

Open the Tokens Studio plugin and navigate to the **settings** page.

* Navigate to the **sync provider** section.
* Select the **local document** option.
* A confirmation dialog appears asking you to **confirm this change**
  * If you select **cancel**
    * The modal will close, and your current sync provider settings will remain.
  * If you select **yes**
    * Tokens currently in the plugin will be stored in the current Figma file
    * The **push** and **pull** actions from the bottom of the plugin won't be available.
      * Changes made to tokens will remain in the current Figma and can't be shared in other Figma files.

<figure><img src="../.gitbook/assets/setting-sync-switch-local-annotated-v2-01 (1).png" alt=""><figcaption></figcaption></figure>

### Your Tokens are now being stored locally

The **Local document** option will show as **active** on the plugin's settings page.

* You can switch back to using a **Sync provider** to store your Tokens remotely at anytime.

{% content-ref url="manage-sync-provider/change.md" %}
[change.md](manage-sync-provider/change.md)
{% endcontent-ref %}



***

### Resources

Community resources:

* None yet!

{% include "../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Sync Local Storage](https://github.com/tokens-studio/figma-plugin/labels/sync%20local%20storage)

{% include "../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* None yet

{% include "../.gitbook/includes/featurebase.md" %}
