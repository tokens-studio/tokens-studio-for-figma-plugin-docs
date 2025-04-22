---
cover: ../../../.gitbook/assets/page-header-figma-import-variables.png
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

# Imported Variable Types and Token Types

## Imported Variable Types and Token Types

Figma has 4 types of Variables, and Tokens Studio supports 24 unique Token Types.&#x20;

When you import Variables into the Plugin, it does not know the correct Token Type to assign to the new Token outside of those 4 Token Types.&#x20;

This means you might have to manually change the `type` of the Token created when you import your Variables. The fastest way to do this is to edit the code files.

#### Change Token Type in Code

Here's a list of the common names of our Token Types, and how they should be written in the code files. For example, a Variable set for Font Family will be imported with the `text` Token Type, because its created as a string variable in Figma.

| Token Type        | Variable Type   | Technical Type in Code                   |
| ----------------- | --------------- | ---------------------------------------- |
| Color             | Color           | `color`                                  |
| Font Family       | String          | `fontFamilies`                           |
| Font Weight       | String / Number | `fontWeights`                            |
| Font Size         | Number          | <p><code>fontSizes</code><br></p>        |
| Line Height       | Number          | <p><code>lineHeights</code><br></p>      |
| Letter Spacing    | Number          | <p><code>letterSpacing</code><br></p>    |
| Paragraph Spacing | Number          | <p><code>paragraphSpacing</code><br></p> |
| Border Radius     | Number          | `borderRadius`                           |
| Border Width      | Number          | `borderWidth`                            |
| Dimension         | Number          | `dimension`                              |
| Spacing           | Number          | `spacing`                                |
| Sizing            | Number          | `sizing`                                 |
| <p>Number<br></p> | Number          | `number`                                 |
| Opacity           | Number          | `opacity`                                |
| Text              | String          | `textCase`                               |
| Boolean           | Boolean         | `color`                                  |

