---
icon: brackets-curly
cover: ../../.gitbook/assets/STUDIO-page-header-sync-provider.png
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

# Tokens Studio Platform - Cloud Sync Provider

## Tokens Studio Platform sync setup guide

Tokens Studio has a **standalone web-based platform** for dynamic creation and management of Design Tokens, currently in Beta!

[→ More information on the Studio Platform and sign up for Beta access here.](https://tokens.studio/studio)



### How it works

* Set up a **project** and **API key** in Tokens Studio
* **Configure Tokens Studio as a sync provider** within the plugin.
* Use the plugin to **sync your Design Tokens** between the Tokens Studio platform and your Figma design files.

<figure><img src="../../.gitbook/assets/sync-studio-platform-header.png" alt=""><figcaption></figcaption></figure>

***

### Tokens Studio sync setup instructions

If you haven't already, sign up for an account at [Tokens Studio](https://app.tokens.studio/)

#### 1. Create a new project

Once you've logged into your Tokens Studio account:

* Select **New Project** from the top-right corner of the home page
  * Give your project a title.
* Now you are looking at the dashboard of your new project.
* Locate the **Connection String** (ID of the project) on the right side of the page
* Use the **copy button** to copy the connection string to your clipboard
* **Save the connection string ID** somewhere safe as it's needed for the plugin configuration.

<figure><img src="../../.gitbook/assets/sync-studio-ConnectionStringID-v2-0 1.png" alt=""><figcaption></figcaption></figure>

#### 2. Create an API key

The **API key** is generated from the Tokens Studio Platform, and acts as a passcode that allows the plugin to connect to your account.

Log into your Tokens Studio Platform account:

* Navigate to your **project dashboard**
* Select the **project name** in the top left corner
* Navigate to **Settings**
* Select **API Keys**
  * Select **Generate API Key**
* Add a **Name** of what the API Key is for.
  * Example: `fimga-sync`
  * Option to add a **Description** for the API Key
    * Example: `test-token sync to plugin`
* Under **Group** select **Admin** which gives you read and write permissions
* Select **create key**
* **Save the generated API key** somewhere safe as it's needed for the plugin configuration.

You're ready to configure the Tokens Studio plugin in Figma!

<figure><img src="../../.gitbook/assets/sync-studio-API Key-v2-0.png" alt=""><figcaption></figcaption></figure>

***

### Configuring Tokens Studio Plugin

In Figma, open the Tokens Studio plugin and navigate to the **Settings** page

* Under the **Sync providers** section, select the **Add new** button to see a list of all Token storage providers
* Select **Tokens Studio**

<figure><img src="../../.gitbook/assets/settings-page-studioplatform-v2-0.png" alt=""><figcaption></figcaption></figure>

#### Add credentials for Tokens Studio sync

You'll need the information saved from the steps above to complete the Tokens Studio sync configuration form.

<figure><img src="../../.gitbook/assets/sync-studio-annotated-v2-0.png" alt=""><figcaption></figcaption></figure>

**1. Name**

This is a **nickname** that shows up in the **plugin settings page** later on to identify this specific sync provider configuration.

* Choose something memorable to you and your project.
* Example: `Hyma brand exploration`



**2. API Key**

The **API Key** you saved from [step 2 above](sync-cloud-studio-platform.md#id-2.-create-an-api-key).



**3. ID (connection string)**

Enter the **Connection String ID** you saved from [step 1 above](sync-cloud-studio-platform.md#id-1.-create-a-new-project).

* This can typically be found in the project section of your Tokens Studio sync dashboard.



#### Save and do the initial sync

Save to confirm your credentials, and follow the prompts in the plugin to finish setting up the Tokens Studio Platform sync.

***

### Shared source of truth

As you work in the plugin, it will continuously update the Studio platform to stay in sync without manual push or pull actions needed.

{% include "../../.gitbook/includes/transforming-tokens.md" %}

***

### Resources

Mentioned in this doc:

* Tokens Studio Platform - https://tokens.studio/studio
* SD-Transforms - [Read Me](https://github.com/tokens-studio/sd-transforms#readme)
* Style Dictionary - https://styledictionary.com/



Community resources:

* None yet!

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Sync Studio platform](https://github.com/tokens-studio/figma-plugin/labels/sync%20tokens%20studio%20\(beta\))

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* 🧑‍💻 [Sync to external token storage enhancements - Feature Request](https://tokensstudio.featurebase.app/p/sync-external-storage-enhancements)
  * How might we improve the experience of working with sync providers in general?
* ↕️ [Git sync enhancements - push, pull, merge, branching - Feature Request](https://feedback.tokens.studio/p/git-sync-enhancements)

{% include "../../.gitbook/includes/featurebase.md" %}
