---
icon: gitlab
cover: ../../.gitbook/assets/gitlab-page-header-sync-provider.png
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

# GitLab - Git Sync Provider

## Gitlab sync setup guide

[Gitlab](https://gitlab.com/) is a popular option to store Design Tokens in a code repository.

You can use the Tokens Studio plugin native integration with Gitlab to sync your Design Tokens to a repository of your choice.

We support two-way sync, meaning you can use the plugin to:

* **Push** JSON files of Design Tokens to Gitlab
* **Pull** the Tokens stored in Gitlab into any Figma file

This means the Design Tokens living in code are the source of truth for our design decisions that can be shared between design and development teams.

This doc outlines how to set up a Gitlab repository and add it as a **Sync provider** in the plugin.

→ Once set up, you can use the plugin's **Push** and **Pull** features to keep your Tokens in sync. #add-doc-link

### How it works

* Set up a **repository** and **personal access token** in Gitlab
* Configure **Gitlab as a sync provider** within the Tokens Studio plugin.
* Use the plugin to **sync your Design Tokens** between Gitlab and Figma design files.

<figure><img src="../../.gitbook/assets/sync-gitlab-header.png" alt=""><figcaption></figcaption></figure>

***

### Gitlab setup steps

If you haven't already, head over to https://Gitlab.com/ and create a free account.

#### 1. Create new project repository

Sign into your account and navigate to the [Create a new project](https://gitlab.com/new) page.

* Choose a **project name**
* In the **project URL** select the **owner** and choose a **project slug**
  * In the plugin, the **project slug** will act as the repository name
  * Names that are easy to remember and type are ideal
* Select your **Visibility level**
  * `Public` anyone can see it
  * `Private` needs permissions to view
    * Your choice doesn't change the plugin's ability to sync with the repository
* `Initialize project with a README file` needs to be checked
  * This is mandatory because the plugin can not sync to an empty repository
* Confirm by pressing the **Create project** button

<figure><img src="../../.gitbook/assets/sync-gitlab-project repo-createNew-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

You are now looking at your new repository! Well done!

**Save the URL of the repository** somewhere safe as it's needed for the plugin configuration.

<figure><img src="../../.gitbook/assets/sync-gitlab-repourl-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Personal access token

Not to be confused with anything to do with a Design _Token_, a **Personal access token** is a passcode from Gitlab you enter into the plugin that allows the connection to happen.

Log into your Gitlab account:

* Navigate to your [Gitlab account settings](https://gitlab.com/-/user_settings/profile)
  * **Select your avatar** on the top left
  * Select **Edit Profile**
* Select **Access Tokens** from the left sidebar
* Click **Add new token**
* Add a **Name** of what the token is for.
  * Example: `test-token repo sync to tokens studio`
* Select an **Expiration** time frame
* Add a **Description** to remind yourself what you made this token for
* Select scopes
  * Ensure the `API` option is selected if you want the plugin to have **read and write permissions**
* Select **Generate token**
* **Save the generated access token** somewhere safe as it's needed for the plugin configuration.

You're ready to configure the Tokens Studio plugin in Figma!

<figure><img src="../../.gitbook/assets/sync-gitlab-PAT-Fine-part1 (1).png" alt=""><figcaption></figcaption></figure>

***

### Plugin settings for Gitlab

In Figma, open the Tokens Studio plugin and navigate to the **Settings** page using the navigation tab.

* Under the **Sync providers** section, select the **Add new** button to see a list of all Token storage providers
* Select **Gitlab**

<figure><img src="../../.gitbook/assets/settings-page-addGitlab-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

Add credentials for Gitlab

Some of the inputs on the form come from the Gitlab steps above, others aren't so obvious as to where the info comes from.

<figure><img src="../../.gitbook/assets/sync-gitlab-annotated-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

#### **1. Name**

This is a **nickname** that shows up in the **plugin settings page** later on to identify this specific sync provider configuration.

* Choose something memorable to you and your project.
* Example: `UdayGitlab`



#### **2. Personal access token**

The **Personal access token** you saved from  [step 2 above](sync-git-gitlab.md#id-2.-personal-access-token).



#### **3. Repository (owner/repo)**

The URL from the **repository** from the [step 1 above](sync-git-gitlab.md#id-1.-create-new-project-repository) has the **owner/repository** in it after the **gitlab.com/**

For example, if your URL says `https://gitlab.com/amazingdesigner/radixtokens,` you will enter `amazingdesigner/radixtokens` into the form in the plugin.

As a note, be sure to use the URL of your repository and not the tree for the Group/Subgroup for your Project listed in Gitlabs UI as it won't work in the plugin.



#### **4. Branch**

Your engineers might tell you what to add as the **default repository branch** where you will be pushing your Tokens, so if you aren't sure, ask them.

* If you created a new repo following the steps above, you will enter `main`.



#### **5. Token storage location (file/folder path)**

This tells the plugin:

* How to organize your Token JSON files in Gitlab.
  * In a folder of multiple files, or a single file.
* The location of where your Token data is stored.
  * The file or folder's pathway (or name) to sync with.

This setting impacts:

* How engineers can work with our Token files during the Token transformation stage of the design-to-development process.
* May limit edit access of Tokens for other team members using the Tokens Studio plugin.

<figure><img src="../../.gitbook/assets/sync-gitlab-file-folder-both-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

#### **Folder**

The folder option syncs Token data from the plugin into a folder that contains multiple JSON files or subfolders of JSON files.

{% include "../../.gitbook/includes/multi-file-sync.md" %}

{% include "../../.gitbook/includes/folder-themes-hint.md" %}



In the plugin, enter the pathway of the folder where you want the Token data to be stored, which is the **folder name** without any extensions.

For example:

```
tokens
```

Our Gitlab repository will have a folder called `tokens` synced to the Tokens Studio plugin in Figma.

* Each **Token Set** created in the plugin is added to the folder as an individual JSON file.
* Additional data files generated by the plugin are also added to the folder.
  * For example, `themes` configuration.

Recall that storing your Token data in a folder (multi-file sync) is a pro feature.

* If other team members are working with your Tokens and do not have a Pro Licence for Tokens Studio, your Tokens will be **read-only** for them.



#### **File Path**

Setting our Token storage as the **file** option syncs our Token data from the plugin into a single JSON file in code.

Combining Token data into a single file limits engineers' ability to work with **Theme** information when transforming Design Tokens.

→ Learn about the Themes (pro) feature in Tokens Studio here. #add-doc-link/themes-pro

**File** storage might work for you if:

* You are using the free version of Tokens Studio.
* Engineers are not using your Design Tokens in code.

In the plugin, we enter the pathway of the JSON file where we want our Token sets to be stored, which is the **file name** with the `.json` extension.

For example:

```
tokens.json
```

Our Gitlab repository will have a single code file called `tokens.json` synced to the Tokens Studio plugin in Figma.

* Each **Token Set** created in the plugin is combined into this single file in our repository.



#### **6. Base URL (Optional)**

**Base URL** must be added to the Gitlab credentials if your organization is running an **enterprise server**.

Looking at the URL of your repository, if you see a name between **gitlab** and **.com**, your organization is running an enterprise server. For example: `https://gitlab.hyma.com/amazingdesigner/radixtokens`

In this example, the `Base URL` you would enter into the plugin form is:

```
gitlab.hyma.com
```

This tells the plugin to point to the API on this specific URL for our organization.



#### Save and do the initial sync

Once you **Save** your credentials, the plugin will compare your tokens with what's in your repository.

You'll see a modal asking you to **push** or **pull** to Gitlab to 'sync' the plugin data with your repository.

{% include "../../.gitbook/includes/add-new-sync-provider.md" %}

***

### Shared source of truth

As you work in the plugin, push and pull indicators remind you to stay in sync with your Gitlab repository.

{% include "../../.gitbook/includes/push-pull.md" %}

Once your Token JSON files are synced to your Gitlab repo, you have a shared source of truth between Designers and Engineers!

{% include "../../.gitbook/includes/transforming-tokens.md" %}

***

### Resources

#### Mentioned in this doc:

* Gitlab - [https://gitlab.com/](https://gitlab.com/)
* SD-Transforms - [Read Me](https://github.com/tokens-studio/sd-transforms#readme)
* Style Dictionary - [https://styledictionary.com/](https://styledictionary.com/)



#### Community resources:

* None yet!

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Sync Gitlab](https://github.com/tokens-studio/figma-plugin/labels/sync%20gitlab)

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* 🧑‍💻 [Sync to external token storage enhancements - Feature Request](https://tokensstudio.featurebase.app/p/sync-external-storage-enhancements)
  * How might we improve the experience of working with sync providers in general?
* ↕️ [Git sync enhancements - push, pull, merge, branching - Feature Request](https://feedback.tokens.studio/p/git-sync-enhancements)
* 🔐 [Data security info request - Feature Request](https://feedback.tokens.studio/p/data-security-info)

{% include "../../.gitbook/includes/featurebase.md" %}
