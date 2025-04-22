---
icon: hexagon
cover: ../.gitbook/assets/page-header-figma-variables.png
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

# Variables and Tokens Studio

## Manage Variables in Figma with Tokens Studio

If your team is working with Variables in Figma, you can use the Tokens Studio Plugin to attach Design Tokens to Variables (and styles). This allows you to manage your Tokens and Variables in the same place, and easily sync your design decisions to a code repository.



### Guides on working with Variables&#x20;

Select a card below to jump to a comprehensive guide on working with Variables, or scroll down to see the [answers to frequently asked questions ↓](variables-overview.md#frequently-asked-questions).

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Export to Figma</strong> <br>Create Variables from Tokens using the Plugin.</td><td><a href="../.gitbook/assets/card-header-figma-export-overview (1).png">card-header-figma-export-overview (1).png</a></td><td><a href="export/">export</a></td></tr><tr><td><strong>Skipped Variables</strong><br>Troubleshooting tips when creating new variables. </td><td><a href="../.gitbook/assets/card-header-figma-variables-skipped.png">card-header-figma-variables-skipped.png</a></td><td><a href="export/variables-skipped.md">variables-skipped.md</a></td></tr><tr><td><strong>Non-Local Variables (pro)</strong><br>Split variable collections across many Figma files.</td><td><a href="../.gitbook/assets/card-header-figma-files.png">card-header-figma-files.png</a></td><td><a href="non-local-files.md">non-local-files.md</a></td></tr><tr><td><strong>Import from Figma</strong><br>Create Tokens from Variables </td><td><a href="../.gitbook/assets/card-header-figma-import-variables.png">card-header-figma-import-variables.png</a></td><td><a href="import/variables/">variables</a></td></tr><tr><td><strong>Styles with Variable References</strong> </td><td><a href="../.gitbook/assets/card-header-figma-styles-var-references.png">card-header-figma-styles-var-references.png</a></td><td><a href="export/styles-variable-references.md">styles-variable-references.md</a></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>



***

### Frequently Asked Questions

Select a question to reveal the answer.&#x20;

<details>

<summary>Which Token types match the different Variable types?</summary>

Tokens Studio supports 23 unique Token Types and there is only 4 Variable Types. Head to the Export to Figma (overview) guide which shows the relationships.&#x20;

[#supported-token-types](export/#supported-token-types "mention")

</details>

<details>

<summary>How do I make sure my Variables are hidden from publishing and scoped properly using Tokens Studio? </summary>

Tokens Studio is not yet able to control Figma's Scoping or Hide from Publishing features.

You can use the Figma native UI to adjust the desired Scoping and Publishing feature without adverse effects to the attached Tokens.&#x20;

</details>

<details>

<summary>Why isn't Theme switching in the Plugin working? </summary>

Once you Export to Figma as Variables using Themes, you will be required to use Figma's native Mode Switching feature.

The Theme Switcher in the Plugin will not work once those themes are attached to a Variable Collection

</details>



#### Manage Variables using Tokens Studio

<details>

<summary>Why didn't the Plugin create Variable Collections with Modes? I have duplicate Collections I wasn't expecting. </summary>

You need to export to Figma from Themes (pro) in order for the Plugin to be able to create a single collection with multiple modes.&#x20;

Head to the guide on Exporting to Figma from Themes for more details.&#x20;

[themes.md](export/themes.md "mention")

</details>

<details>

<summary>My Variable Collection names aren't what I expected, how do I fix this?</summary>

When Exporting to Figma to create Variables, the Collection Name is created from the Theme Group when exporting from themes, and the Token Set name when exporting from Token Sets. \
\
Head to the guide on Exporting to Figma for more details.&#x20;

[export](export/ "mention")

</details>

<details>

<summary>When creating Variables from Tokens using the Plugin, why are there less Variables then I have Tokens? </summary>

There are many reasons why the Plugin may have to skip creating a Variable. Head to the guides for Skipped Variables when Exporting to Figma for more details.&#x20;

[variables-skipped.md](export/variables-skipped.md "mention")

</details>



#### Create Design Tokens in the Plugin from Variables

<details>

<summary>After importing my variables into the Plugin, I'm confused at how things are organized in Tokens Studio. </summary>

Congrats on getting this far! Head to the comprehensive guide on Importing Variables for some handy visuals and pro-tips.&#x20;

[variables](import/variables/ "mention")

</details>

