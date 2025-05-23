---
icon: github
cover: ../../.gitbook/assets/github-page-header-sync-provider.png
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

# GitHub - Git Sync Provider

## GitHub sync setup guide

[GitHub ](https://github.com/)is a popular Git-based source code repository hosting service.

You can use the Tokens Studio plugin native integration with GitHub to sync your Design Tokens to a repository of your choice.

We support two-way sync, meaning you can use the plugin to:

* **Push** JSON files of Design Tokens to GitHub
* **Pull** the Tokens stored in GitHub into any Figma file

{% include "../../.gitbook/includes/push-pull.md" %}

This means the Design Tokens living in code are the source of truth for our design decisions, which can be shared between design and development teams.

This guide outlines how to set up a GitHub repository and add it as a **Sync provider** in the plugin.

### How it works

* Set up a **repository** and **personal access token** in GitHub
* Configure **GitHub as a sync provider** within the Tokens Studio plugin.
* Use the plugin to **sync your Design Tokens** between GitHub and Figma design files.

<figure><img src="../../.gitbook/assets/sync-github-header.png" alt=""><figcaption></figcaption></figure>

***

### GitHub setup steps

If you haven't already, head over to [https://GitHub.com/](https://github.com/) and create a free account.

#### 1. Create a new repository

Sign into your account and navigate to the [Create a new repository](https://github.com/new) page.

* Choose a specific and memorable **repository name** which will be used in the plugin as the destination for your Design Tokens.
  * Names that are easy to remember and type are ideal
* Select if you want your repository to be:
  * `Public` anyone can see it
  * `Private` needs permissions to view
    * Your choice doesn't change the plugin's ability to sync with the repository
* `Add a README file` needs to be checked
  * This is mandatory because the plugin can not sync to an empty repository.
* Add .gitignore can be **None**
* Choose a licence can be **None**
* Confirm by pressing the **Create repository** button

You are now looking at your new repository! Well done!

<figure><img src="../../.gitbook/assets/sync-github-repo-createNew-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

**Save the URL of the repository** somewhere safe as it's needed for the plugin configuration.

<figure><img src="../../.gitbook/assets/sync-github-repourl-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Personal access token

Not to be confused with anything to do with a Design _Token_, a **Personal access Token** is a passcode from GitHub you enter into the plugin that allows the connection to happen.

Log into you GitHub account:

* Navigate to your [GitHub account settings](https://github.com/settings/profile)
  * **Select your avatar** on the top right
  * Select **Account Settings**
* Select **Developer Settings** from the bottom of the options
* Select **Personal Access Tokens** to see the two options, either will work:
  * **Fine-grained Tokens**
    * Repository-specific detailed access Tokens.
  * **Tokens (classic)**
    * Less specific, one PAT provides access to multiple repositories.

**Generate a new classic access token**

* Select **Generate new token (beta)**
* Add a **Note** of what the token is for.
  * Example: `test-token repo sync to tokens studio`
* Select an **Expiration** time frame
* Select **scopes** for access
  * `repo` parent checkbox is the minimum requirement for the plugin
* Scroll down to the bottom and select **Generate token**
  * **Save the generated access token** somewhere safe as it's needed for the plugin configuration.

You're ready to configure the Tokens Studio plugin in Figma!

<figure><img src="../../.gitbook/assets/sync-github-PAT-Classic (1).png" alt=""><figcaption></figcaption></figure>

#### **Generate new fine-grained access token**

* Select **Generate new token (beta)**
* Add a **Name** of what the token is for.
  * Example: `test-token repo sync to tokens studio`
* Select an **Expiration** time frame
* Add a **Description** to remind yourself what you made this token for
* Choose your **Repository access**
  * Decide between `All` or `select` repositories

<figure><img src="../../.gitbook/assets/sync-github-PAT-Fine-part1 (1).png" alt=""><figcaption></figcaption></figure>

Select your **Repository permissions**

* Find **Contents** and open the dropdown
  * `Read and Write` is required for creating and editing tokens stored in your repository
  * `Read-only` would allow you to view Tokens stored in code in the plugin, but not create or edit them.
    * Maybe helpful for product designers who just want view access of your Tokens for theme switching and applying Tokens for example.
* Scroll down to the bottom and select **Generate token**
* **Save the generated access token** somewhere safe as it's needed for the plugin configuration and you won't see it again once you leave the current GitHub page.

You're ready to configure the Tokens Studio plugin in Figma!

<figure><img src="../../.gitbook/assets/sync-github-PAT-Fine-part2 (1).png" alt=""><figcaption></figcaption></figure>

***

### Plugin settings for GitHub

In Figma, open the Tokens Studio plugin and navigate to the **Settings** page using the navigation tab.

* Under the **Sync providers** section, select the **Add new** button to see a list of all Token storage providers
* Select **GitHub**

<figure><img src="../../.gitbook/assets/settings-page-addGithub-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

#### Add credentials for GitHub

Some of the inputs on the form come from the GitHub steps above, others aren't so obvious as to where the info comes from.

<figure><img src="../../.gitbook/assets/sync-github-annotated-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

#### **1. Name**

This is a **nickname** that shows up in the **plugin settings page** later on to identify this specific sync provider configuration.

* Choose something memorable to you and your project.
* Example: `Radix - Community token files`



**2. Personal access token**

The **Personal access token** you saved in [step 2 above](sync-git-github.md#id-2.-personal-access-token).



**3. Repository (owner/repo)**

The URL from the **repository** [you recorded in step 1 above](sync-git-github.md#id-1.-create-a-new-repository) has the **owner/repository** in it after the **GitHub.com/**

For example, if your URL says `https://GitHub.com/amazingdesigner/radixtokens`, you will enter `amazingdesigner/radixtokens` into the form in the plugin.



**4. Branch**

Your engineers might tell you what to add as the **default repository branch** where you will be pushing your Tokens, so if you aren't sure, ask them.

* If you created a new repo following the steps above, you will enter `main`.
* You can create additional branches using the plugin later.



**5. Token storage location (file/folder path)**

This tells the plugin:

* How to organize your Token JSON files in GitHub.
  * In a folder of multiple files, or a single file.
* The location of where your Token data is stored.
  * The file or folder's pathway (or name) to sync with.

This setting impacts

* How engineers can work with our Token files during the Token transformation stage of the design-to-development process.
* May limit edit access of Tokens for other team members using the Tokens Studio plugin.

<figure><img src="../../.gitbook/assets/sync-github-file-folder-both-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

**Folder**

The folder option syncs Token data from the plugin into a folder that contains multiple JSON files or subfolders of JSON files.

{% include "../../.gitbook/includes/multi-file-sync.md" %}

{% include "../../.gitbook/includes/folder-themes-hint.md" %}



In the plugin, enter the pathway of the folder where you want the Token data to be stored, which is the **folder name** without any extensions.

For example:

```
tokens
```

Our GitHub repository will have a folder called `tokens` synced to the Tokens Studio plugin in Figma.

* Each **Token Set** created in the plugin is added to the folder as an individual JSON file.
* Additional data files generated by the plugin are also added to the folder.
  * For example, `themes` configuration.

Recall that storing your Token data in a folder (multi-file sync) is a pro feature.

* If other team members are working with your Tokens and do not have a Pro Licence for Tokens Studio, your Tokens will be **read-only** for them.



**File Path**

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

Our GitHub repository will have a single code file called `tokens.json` synced to the Tokens Studio plugin in Figma.

* Each **Token Set** created in the plugin is combined into this single file in our repository.



**6. Base URL (Optional)**

**Base URL** must be added to the GitHub credentials if your organization is running an **enterprise server**.

Looking at the URL of your repository, if you see a name between **GitHub** and **.com**, your organization is running an enterprise server. For example: `https://github.hyma.com/amazingdesigner/radixtokens`

In this example, the `Base URL` you would enter into the plugin form is:

```
github.hyma.com
```

This tells the plugin to point to the API on this specific URL for our organization.



#### Save and do the initial sync

Once you **Save** your credentials, the plugin will compare your Tokens with whats in your repository.

You'll see a modal asking you to **push** or **pull** to GitHub to 'sync' the plugin data with your repository.

<figure><img src="../../.gitbook/assets/sync-git-push-pull-modal-v2-0 (1).png" alt=""><figcaption></figcaption></figure>

{% include "../../.gitbook/includes/add-new-sync-provider.md" %}

***

### Shared source of truth

As you work in the plugin, **push** and **pull** indicators remind you to stay in sync with your GitHub repository.

{% include "../../.gitbook/includes/push-pull.md" %}

Once your Token JSON files are synced to your GitHub repo, you have a shared source of truth between Designers and Engineers!

{% include "../../.gitbook/includes/transforming-tokens.md" %}

***

### Resources

Mentioned in this doc:

* [Github](https://github.com/)
* SD-Transforms - [Read Me](https://github.com/tokens-studio/sd-transforms#readme)
* Style Dictionary - [https://styledictionary.com/](https://styledictionary.com/)



#### Community resources:

* None yet!

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Github Sync](https://github.com/tokens-studio/figma-plugin/labels/sync%20github)

* Push/pull indicator persists with GitHub Sync [#2320](https://github.com/tokens-studio/figma-plugin/issues/2320)
  * Occasionally you have to push/pull to GitHub several times for the indicator to clear.

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* 🧑‍💻 [Sync to external token storage enhancements - Feature Request](https://tokensstudio.featurebase.app/p/sync-external-storage-enhancements)
  * How might we improve the experience of working with sync providers in general?
* ↕️ [Git sync enhancements - push, pull, merge, branching - Feature Request](https://feedback.tokens.studio/p/git-sync-enhancements)
* 🔐 [Data security info request - Feature Request](https://feedback.tokens.studio/p/data-security-info)

{% include "../../.gitbook/includes/featurebase.md" %}
