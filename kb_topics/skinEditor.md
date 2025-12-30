# Skin Editor

[← Back to API Index](../reference.md)

---

## KB Topic: Skin Editor

### Description
#### Rapid skin customization
Isomorphic provides a visual Skin Editor tool which allows for rapid, bulk customization of skin details like colors, borders and fonts. With this tool, you can create a new skin based on an existing one, customize it and then export it to a zip file that you can drop into any SmartClient project.

Your changes are saved in an intermediate database so the skin can be updated over time. When you are happy with your skin, export it to a zip file, drop it into your project skins/ directory and load it as you would any other skin. See below for details on exporting.

You can access the Skin Editor in one of two ways:

#### Online
The Skin Editor is available online as a single-user tool at [smartclient.com/themes](https://www.smartclient.com/themes/). This link runs against the [latest public release](https://www.smartclient.com/product/download.jsp) and is available to customers with a [Pro or better](https://www.smartclient.com/product/) license of that release. Note that this is a single-user version of Skin Editor and does not support some team features like sharing your design with other users.

For Skin Editor team support, registered users can access the tool via [Reify](https://create.reify.com), Isomorphic's low-code platform. The [Skin Editor for Reify](https://create.reify.com/themes/) allows skin-designs to be shared among users and changes you make to your skins are reflected right away within `Reify`. Note that this version of the tool may be running bleeding-edge code, more recent then the current public release.

#### Locally
If you have a [Pro or better](https://www.smartclient.com/product/) license, you can access the Skin Editor by clicking the `Skin Editor` icon in the SmartClient SDK Explorer, or by navigating to `tools/skinTools/skinEditor.jsp`.

#### Prerequisites
Using Skin Editor locally requires the following additional steps:

*   the builtin DataSource `userSkin` must be imported to your Database using the [adminConsole](adminConsole.md#kb-topic-admin-console). This DataSource is used to store user skins until export
*   both [Ruby](http://www.ruby-lang.org/en/downloads/) and [Compass](http://compass-style.org/install/) need to be installed on your computer, and in the PATH. During saves, Skin Editor uses `Compass` to recompile skin-CSS, via an operation on the `userSkin` DataSource which invokes _**compass compile 'path-to-skin-template-dir'**_ on the server.

#### Exporting Skins
To export a skin, load it in the Skin Editor and click the "Export" button to download the skin in a zip file. To use the skin, extract the zip into your project skins/ directory and load it in your project in the usual way.

A skin exported in this way can be further edited locally in your project Skin Editor, if you have an appropriate license. Once extracted into the skins/ directory, it will appear in Skin Editor's list of user-skins and can be edited as normal, with changes being saved to disk rather than database. You might want to do this, for example, in order to make non-CSS configuration to the skin, via `load_skin.js`. While future versions of Skin Editor will support non-CSS skin configuration, these features are not yet available.

#### Base Skins
When you create a new skin in Skin Editor, the first step is to choose a Base skin to use as a starting-point - by default, these are all builtin Isomorphic skins, but you can add your own to the list by selecting _Export as a Base skin_ in the Skin Editor.

You might want to do this if you create a customized skin and you want to be able to generate several variations on it - like changing colors, to make the color schemes of multiple customers that you are creating applications for.

---
