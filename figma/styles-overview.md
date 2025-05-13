---
icon: grid-round-2
cover: ../.gitbook/assets/page-header-figma-styles.png
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

# Styles and Tokens Studio

## Manage Styles in Figma with Tokens Studio&#x20;

If your team is working with Styles in Figma, you can use the Tokens Studio Plugin to attach Design Tokens to Styles (and Variables). This allows you to manage your Tokens and Styles in the same place, and easily sync your design decisions to a code repository.\


### Guides on working with Styles&#x20;

Select a card below to jump to a comprehensive guide on working with Styles, or scroll down to see the[ answers to frequently asked questions ↓](styles-overview.md#frequently-asked-questions).

<table data-view="cards"><thead><tr><th></th><th data-hidden data-card-cover data-type="files"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td><strong>Export to Figma</strong><br>Create Styles from Tokens using the Plugin.</td><td><a href="../.gitbook/assets/card-header-figma-styles.png">card-header-figma-styles.png</a></td><td><a href="export/">export</a></td></tr><tr><td>Create <strong>Styles with Variable References</strong><br></td><td><a href="../.gitbook/assets/card-header-figma-styles-var-references.png">card-header-figma-styles-var-references.png</a></td><td><a href="export/styles-variable-references.md">styles-variable-references.md</a></td></tr><tr><td><strong>Import from Figma</strong><br>Create Tokens from Styles</td><td><a href="../.gitbook/assets/card-header-figma-import-styles.png">card-header-figma-import-styles.png</a></td><td></td></tr></tbody></table>





***



### Frequently Asked Questions

&#x20;Select a question to reveal the answer.&#x20;

<details>

<summary>Which Token Types match the different Style types?</summary>

Tokens Studio supports 23 unique Token Types and there is only 4 Style Types. Head to the Export to Figma (overview) guide which shows the relationships.&#x20;

[#supported-token-types](export/#supported-token-types "mention")

</details>



#### Manage Styles using Tokens Studio&#x20;

<details>

<summary>I exported my Typography Tokens as Text Styles using the plugin, how can I get variables linked to the text properties of the styles in figma? </summary>

This workflow is covered in the comprehensive guide to creating Styles with Variable References.&#x20;

[styles-variable-references.md](export/styles-variable-references.md "mention")

</details>



#### Create Design Tokens in the Plugin from Styles

<details>

<summary>I've imported styles with Variable values, why aren't the references in the Tokens created in Tokens Studio?</summary>

This is a known limitation of the Plugin.&#x20;

You can still import them but any connection to Variables will need to be manually created. Head to the Import Styles guide for more details.&#x20;

[styles.md](import/styles.md "mention")

</details>



{% include "../.gitbook/includes/spacer-image-fullwidth.md" %}
