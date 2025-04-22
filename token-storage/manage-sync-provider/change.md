---
icon: arrow-pointer
cover: ../../.gitbook/assets/SELECT-page-header-sync-provider.png
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

# Change Active Sync Provider

## Change the active sync provider

Once you have added one or more Sync Providers to Tokens Studio, you can switch between sync providers or temporarily store your Tokens locally in the Figma file.

### In the plugin

Open the Tokens Studio plugin and navigate to the **settings** page.

1. Navigate to the **sync provider** of your choice in the list.
2. Select the **apply button** on the right side of the **sync provider** details.

<figure><img src="../../.gitbook/assets/setting-sync-switch-localRemote-annotated-v2-01.png" alt=""><figcaption></figcaption></figure>

#### Remote storage providers

After selecting a different storage provider from your list of options, the plugin will compare your Tokens with what is in your remote storage.

You may see a modal asking you to **push** or **pull** to 'sync' the plugin data with your storage provider, depending on the type of provider, permissions, and the Tokens you have in the plugin.

These images show the **push** and **pull** modals for a new GitHub sync, but it will look similar for most providers.

<figure><img src="../../.gitbook/assets/sync-git-push-pull-modal-v2-0 (2).png" alt=""><figcaption></figcaption></figure>

**Pull from provider**

If your sync provider already has Design Tokens, you'll see a dialogue asking if you want to **pull** your Tokens in.

* If you select **yes**
  * Tokens in your remote storage will be **pulled** into the plugin.
  * Any Tokens currently in the plugin will be replaced with the Tokens in your remote storage, and they can not be recovered.
  * Once the pull is complete, the modal will close and you'll be returned to the **Settings** page of the plugin.
* If you select **cancel**
  * Tokens currently in the plugin will remain, and you can choose to push them to your sync provider later.
  * The modal will close and you'll be returned to the **Settings** page of the plugin.
* If you close the modal without making a selection
  * Tokens currently in the plugin will remain, and you can choose to push them to your sync provider later.
  * Closing the modal returns you to the **Settings** page of the plugin.

{% include "../../.gitbook/includes/push-pull.md" %}

**Push from local**

If your sync provider does not have code files with Design Tokens, you'll see a modal asking if you want to **push**.

This would **push** or "send" the current Tokens in the plugin to your sync provider.

* If you select **Push changes**
  * The **commit message** is required.
    * You can think of it as a short note to your engineers about what you are **pushing**, such as "initial token load."
  * Tokens in the plugin will be **pushed** to your remote storage.
  * Once the pull is complete, the modal will close and you'll be returned to the **Settings** page of the plugin.
* If you select **cancel**
  * Tokens currently in the plugin will remain, and you can choose to push them to your sync provider later.
  * The modal will close and you'll be returned to the **Settings** page of the plugin.
* If you close the modal without making a selection
  * Tokens currently in the plugin will remain, and you can choose to push them to your sync provider later.
  * Closing the modal returns you to the **Settings** page of the plugin.

***

### Resources

Community resources:

* None yet!

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - Open issues for [Sync Providers Manage](https://github.com/tokens-studio/figma-plugin/labels/sync%20providers%20manage)

* None yet

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* None yet

{% include "../../.gitbook/includes/featurebase.md" %}
