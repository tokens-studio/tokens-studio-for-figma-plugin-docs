---
icon: input-text
cover: ../../.gitbook/assets/pageHeader-anatomy-tokenName-technicalSpec.png
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

# Token Name Technical Specs

## Design Token Name Technical Specifications

The `name` of a Design Token acts as the unique identification for our design decisions in code.

<figure><img src="../../.gitbook/assets/token-anatomy-name.png" alt=""><figcaption><p>In this infographic, the Token examples on the right side highlight the Name. The top code block shows a Token Name with groups. The bottom code block shows a flat Token Name.</p></figcaption></figure>



While naming is a personalized part of working with Design Tokens, we've compiled guidelines to avoid common naming errors that cause technical issues for engineers.

This information is based on:

* [Technical specifications](https://tr.designtokens.org/format/#name-and-value) outlined in the latest W3C draft by the Design Tokens Community Group.
* The most common issues with Token Names while transforming for code provided by the [Style Dictionary](https://styledictionary.com/) engineering team.

Knowing how things work "under the hood" can help you make better choices when choosing names for Tokens to avoid errors when your Tokens are used in code.&#x20;

{% hint style="info" %}
While there aren't official specifications for naming Token Sets, the same best practices for naming your Tokens will also apply to naming your Token Sets.&#x20;
{% endhint %}

***



### Tokens are case sensitive

Tokens with the same names but different uses of capital letters will be seen in the system as unique Design Tokens.

For example, all of these Tokens would be viewed as unique Tokens by a back-end system: `tokenName` `tokenname` `Tokenname` `TokenName`

You'll want to decide on a casing strategy for your Token's names and stick with it.



### Tokens can be grouped by Name

The period (.) character is used to create **Groups of Tokens**. Grouping Tokens helps to organize your Tokens into a tree structure in your design tools and code files.

You can think of the Groups in Token Names as a _folder system_ for your design decisions.

For example, these **Color Tokens** do not have any grouping, also known as **Flat** names:

```json
colors-green-100
colors-green-200
colors-green-300
```

Compared to grouped names, which replaces the dash (`-`) with a period (`.`):

```json
colors.green.100
colors.green.200
colors.green.300
```

These 3 Tokens would end up being grouped in JSON file:

````json
{
  "colors": {
    "green": {
      "100": {
        "value": "#0e1512",
        "type": "color"
      },
      "200": {
        "value": "#121b17",
        "type": "color"
      },
      "300": {
        "value": "#132d21",
        "type": "color"
      }
    }
  }
}
```
````

In Tokens Studio, there are workflow features for [Token Groups](groups.md) which allow you take bulk actions on an entire Group (any any subgroups).&#x20;



### **Reserve periods for creating groups**

When creating your Token names, be sure to use period (`.`) where you want to create a Group and not to represent the identification of a design decision.

This is a common mistake when creating Token Names for dimension properties where a scale needs a half or quarter step.

For example, a half step between `spacing.1` and `spacing.2` is commonly written as `spacing.1.5` or `spacing.1-5`

However, both of these options are less than ideal once we pass our Tokens over to engineers who modify our Token Names as a part of the Transformation process.



***



### Token names are modified by engineers

Engineers use a tool like [Style Dictionary](https://amzn.github.io/style-dictionary/#/) to transform Design Tokens into whatever specific formats they need.

During the transformation process, they often modify the Token names to match their preferred workflow.

Most common Token name modifications:

* Change casing and punctuation.
* Flatten them to remove groups.
* Add or remove front matter/prefixes.
* Remove designer-specific words.

For example, if the engineer writes their code in `camelCase`, your Design Tokens would change:

* Original: `my-awesome-token`
* Transformed: `myAwesomeToken`

So when you write your Token names in the plugin without any issues, once engineers modify them, there could be multiple tokens with the same name.

This could be a problem that causes naming collisions because your engineer no longer has a unique ID for each design decision.

| Original Name | Flattened Name |
| ------------- | -------------- |
| spacing.1.5   | spacing15      |
| spacing.1-5   | spacing15      |
| spacing.15    | spacing15      |



### Names act as the unique ID for each design decision

It's important to be thoughtful with your naming structure to ensure each Design Token has a unique name, which acts as the identifier for a specific design decision.

If there are more than one identical Token names with different values, the system doesn't know which ID to pay attention to.

This is called a **naming collision**, which can be intentional.

In the case of theming, we have multiple Token sets containing Tokens with identical names but different values. We tell the system which theme is active, and it overrides all Tokens with the chosen values.

For example, a person selects dark mode on a website and all the components are styled based on the dark-theme Tokens in the backend.

This can also be unintentional.

The spacing Tokens from the earlier example might be written like this in Tokens Studio:

```json
spacing.1
spacing.1-5
spacing.2
...
spacing.15
```

When flattened by engineers to remove dashes (`-`) and periods (`.`) in the transformation process, it would result in these Token Names:

```json
spacing1
spacing15
spacing2
...
spacing15
```

Which causes a naming collision for `spacing15`.

So, to avoid this issue when working with numeric scales, you could write the name of the fraction as a string.

For example, `spacing.1-5` could be `spacing.1half`.

When the same Tokens from above are flattened, they would appear as:

```json
spacing1
spacing1half
spacing2
...
spacing15
```

***



### Things to avoid

When creating your Token Names, you'll want to avoid strings that are considered "forbidden" because they can cause destructive issues in code.



#### Forward slash - /

Figma uses the forward slash to create groups and folders to organize [components](https://help.figma.com/hc/en-us/articles/360038663994-Name-and-organize-components), [styles](https://help.figma.com/hc/en-us/articles/360039820134-Manage-and-share-styles#Group_styles) and [variables](https://help.figma.com/hc/en-us/articles/15145852043927-Create-and-manage-variables#01H8044A3JN28S65BS0G7Q9E19)

In Tokens Studio, when you use a period (`.`) to create token groups and export them to Figma, the plugin converts the period to forward slash (`/`) to create the same groups in Figma automagically.

So, to avoid creating unintentional groups in Figma, do not use forward slashes (`/`) when writing your Token names.

{% hint style="info" %}
When naming a Token Set, this rule does not apply. In the Tokens Studio plugin for Figma if you name your Token Sets with a `/` , the `/` creates the group, or folder structure for your JSON files.&#x20;
{% endhint %}



#### Dollar sign - $

In your Token JSON files, an object with the dollar sign has an assigned property in the Design Tokens spec, typically the parts identified in the Anatomy of a Design Token (more on that below).

Examples:

* `"$description"` denotes the property of token description
* `"$type"` denotes the type of token

> [The DTCG Spec states](https://tr.designtokens.org/format/#character-restrictions): "...token and [group](https://tr.designtokens.org/format/#groups) names _MUST NOT_ begin with the `$` character."

This means that Token names can't begin with the `$` character but could technically exist in other parts of the name. We suggest you avoid it whenever possible to avoid complications in code.



#### Names that match Token anatomy

Avoid using names that match the official anatomic parts of a Token, as these specific strings of text are reserved for functional logic when using Tokens in code:

* `name`
* `type`
* `value`
* `description`

One of the most common errors in naming Tokens happens with Typography design decisions being shortened to include the word `type` as a shortform for Typography.



#### Curly brackets - { }

Curly brackets are used to identify Tokens with Values that reference another Token. #add-doc-link/token-values-references

Example: `"$value": "{green-500}"`

So if they are also in a Token Name it totally breaks the code. This is common when folks are trying to reference a keyword in a Token Name by using curly brackets, which is a clever idea, but problematic for the plugin to process and for engineers to work with.



#### Square and round brackets - \[ ] ( )

Much like the curly brackets, square and round brackets are often used in code, and when we include them in our Token names it leads to undesirable results.



#### Special characters, emojis and spaces - 😳

When transforming tokens in code, using spaces, emoji or special characters can cause problems and a lot of unnecessary custom transformations to fix.

This issue often happens when importing Styles or Variables from Figma into the Plugin. While designers might find adding emoji's and special characters to their Figma workflow, they are not suitable for use in Design Tokens, which are technically code.

***



### Resources

Mentioned in this doc:

* SD-Transforms - [Read Me](https://github.com/tokens-studio/sd-transforms#readme)
* Style Dictionary -[ https://styledictionary.com/](https://styledictionary.com/)
* Design Tokens Community Group - [W3C Draft](https://tr.designtokens.org/format/)
* Design Tokens Community Group - [W3C Draft, 5.1 Name and Value](https://tr.designtokens.org/format/#name-and-value)
* Design Tokens Community Group -[ W3C Draft, 3.7 Group](https://tr.designtokens.org/format/#group)

#### Figma resources:

* Figma - [Name and Organize Components](https://help.figma.com/hc/en-us/articles/360038663994-Name-and-organize-components)
* Figma - [Manage and Share Styles](https://help.figma.com/hc/en-us/articles/360039820134-Manage-and-share-styles#Manage_styles)
* Figma - [Create and Manage Variables](https://help.figma.com/hc/en-us/articles/15145852043927-Create-and-manage-variables#01H8044A3JN28S65BS0G7Q9E19)



#### Community resources:

* None yet

{% include "../../.gitbook/includes/something-to-share-subm....md" %}



#### Known issues and bugs

Tokens Studio Plugin GitHub - [Open issues for Token Names](https://github.com/tokens-studio/figma-plugin/labels/token%20name)

{% include "../../.gitbook/includes/bug-report.md" %}



#### Requests, roadmap and changelog

* None yet

{% include "../../.gitbook/includes/featurebase.md" %}
