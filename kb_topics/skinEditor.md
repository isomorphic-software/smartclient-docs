# Skin Editor

[← Back to API Index](../reference.md)

---

## KB Topic: Skin Editor

### Description
Isomorphic provides a visual Skin Editor tool which allows for rapid, bulk customization of skin details like colors, borders and fonts.

With this tool, you can create a new skin based on an existing one and make styling customizations to it - your changes are saved in an intermediate database so the skin can be updated over time. If the skin exists in a local SDK Skin Editor and your project uses the [SmartClient Server](iscServer.md#kb-topic-smartclient-server-summary), it can be loaded by pages outside of the Skin Editor in the same way as any other skin. The server delivers your saved Skin Editor customizations from the database as if the skin existed on disk.

Once complete, you can choose to leave your skin in the Skin Editor database, if it's local, or export it to a zip file that can be dropped into your project skins/ directory, along with other framework skins. If you export as a "Base" skin, your customizations are exported as base config and the skin is no longer editable in the Skin Editor - if you export as a "User" skin, you can extract the zip to another environment where it will continue to be editable if that environment has a local Skin Editor, by selecting it from the "Edit Skin" picker. This means that the exported zip must not be extracted into the same environment as the Skin Editor, since skin-names must be unique. See below for details on exporting.

#### Accessing Skin Editor
You can access the Skin Editor in one of two ways:
#### Online
The Skin Editor is available online as a single-user tool at [smartclient.com/themes](https://www.smartclient.com/themes/). This link runs against the [latest public release](https://www.smartclient.com/product/download.jsp) and is available to customers with a [Pro or better](https://www.smartclient.com/product/) license of that release. Note that this is a single-user version of Skin Editor and does not support some team features like sharing your design with other users.

For Skin Editor team support, registered users can access the tool via [Reify](https://create.reify.com), Isomorphic's low-code platform. The [Skin Editor for Reify](https://create.reify.com/themes/) allows skin-designs to be shared among users and changes you make to your skins are reflected right away within `Reify`. Note that this version of the tool may be running bleeding-edge code, more recent then the current public release.

#### Locally
If you have a [Pro or better](https://www.smartclient.com/product/) license, the Skin Editor is shipped with your SDK, in the `/tools/skinEditor/` directory. You can run the tool by navigating to `tools/skinTools/skinEditor.jsp` or by clicking the `Skin Editor` icon in the SmartClient SDK Explorer.

#### Creating a new skin
To create a new skin in the Skin Editor, select a Base-skin from the grid and enter a name for your skin. The name must be unique across all existing User-skins, including those in the `isc_userSkin` dataSource and those on-disk.

#### The main screen
When you're ready, click the "Create and Edit Skin" button to advance to the main editor screen, which consists of two main panels.

*   On the left, a set of [tabs](../classes/TabSet.md#class-tabset), each housing trees with cascades of skin settings such as colors, borders and padding. Above these is a [ColorItem](../classes/ColorItem.md#class-coloritem) labelled "Highlight Color", which is the main color from which most of the colored parts of the skin inherit - for example, background colors in [ListGrid](../classes/ListGrid_1.md#class-listgrid) headers and rollovers, backgrounds and shadows of buttons of various types, and various cases where text is highlighted, such as values with [unsaved changes](../classes/FormItem.md#attr-formitemshowpending). Above this ColorItem are several functional buttons: "Delete", which permanently removes a skin; "Export", which allows the skin to be exported to a zip file for distribution; and "Save", which saves your changes to database or file-system where you skin exists and recompiles the underlying stylesheet to include your changes.
*   On the right, a "Preview" area showing some sample components. Above this area is a toolbar offering a selector to change between which types of components to show in the Preview, a selector for modifying the "Density" (size/spacing) of the skin, and a button for switching all components in the Preview into a "Disabled" state, in order to understand those styles.

#### Editing a skin
To make modifications to your skin, change values in the trees on the left to see your changes applied to the widgets in the Preview area on the right. Changing values higher up in the cascades, such as "Standard Text", is a good place to start because those values will affect the broadest set of variables with the fewest changes - more specific changes can be applied in later passes.

As a rough guide, a good way to start is as follows:

*   "Standard Background Color" - this cascades to the entire skin and sets up whether your skin is essentially a light or dark skin
*   "Standard Text Color" - this cascades to most of the skin and is typically dark-grey to black in lighter skins, or light-grey to white in darker skins
*   "Standard Border Color" - this cascades to most of the skin - it's typically a light-grey and largely uniform across a skin, where borders are present
*   "Highlight Color" - if this color is blue and you change it to green, most colors in the skin that were previously a shade of blue will change to a shade of green - this might include background/rollover-colors, text, shadows or focused borders, for example, in any widget

As you make changes, you'll see them applied in the Preview area on the right of the screen. Use the "Select View" picker above the Preview to show different types of widgets and discover how your changes affect them.

The Skin Editor only allows for editing variables which are used to populate the base skin's SASS template. It will incorporate your changes to those template variables and recompile the content for the skin's stylesheet, `skin_styles.css`, but it does not currently allow for customizing the other parts of the skin, such as JavaScript code and icons.

#### Skin Editor files
Files used by the Skin Editor include:

*   skinEditor.jsp - the bootstrap page for the tool
*   colorTester.jsp - the page displayed in the Skin Editor's _Preview Pane_

In addition to these application files, the tool requires several framework [DataSource](../classes/DataSource.md#class-datasource)s

*   _isc\_baseSkin_ - manages information about "base" skins, which are skins that can be used as the starting point for custom skins in the Skin Editor. The _Flat series_ of framework skins are base-skins.
*   _isc\_userSkin_ - manages information about "user" skins, which are custom skins created in the Skin Editor, as an extension of an existing _base_ skin. These user skins can exist either as dataSource-records or as exported skins on disk.
*   _isc\_registeredFonts_ - manages information about fonts which have been registered with the framework and exist in the `system/helpers/fonts` directory. These are the fonts available in the Skin Editor.

#### Prerequisites
Using Skin Editor locally requires the following additional steps:

*   the builtin DataSource `isc_userSkin` must be imported to your Database using the [adminConsole](adminConsole.md#kb-topic-admin-console). This DataSource is used to store user skins until export
*   [python](https://www.python.org/downloads/), [Ruby](http://www.ruby-lang.org/en/downloads/) and [Compass](http://compass-style.org/install/) must all be installed on your computer, and in the PATH. During saves, Skin Editor uses `Compass` to recompile skin-CSS, via an operation on the `isc_userSkin` DataSource which invokes _**compass compile 'path-to-skin-template-dir'**_ on the server.

#### Exporting Skins
To export a skin, load it in the Skin Editor and click the "Export" button to download the skin in a zip file. To use the skin, extract the zip into your project skins/ directory and load it in your project in the usual way.

A skin exported in this way can be further edited locally in your project Skin Editor, if you have an appropriate license. Once extracted into the skins/ directory, it will appear in Skin Editor's list of user-skins and can be edited as normal, with changes being saved to disk rather than database. You might want to do this, for example, in order to make non-CSS configuration to the skin, via `load_skin.js`. While future versions of Skin Editor will support non-CSS skin configuration, these features are not yet available.

#### Base Skins
When you create a new skin in Skin Editor, the first step is to choose a Base skin to use as a starting-point - by default, these are all builtin Isomorphic skins, but you can add your own to the list by selecting _Export as a Base skin_ in the Skin Editor.

You might want to do this if you create a customized skin and you want to be able to generate several variations on it - like changing colors, to make the color schemes of multiple customers that you are creating applications for.

---
