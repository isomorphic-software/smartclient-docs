# skins

[← Back to API Index](../reference.md)

---

## KB Topic: skins

### Description
Skins are a collection of styles, images and other settings used to manage the overall appearance of an application.

A skin is typically in a single directory and consists of:

*   _load\_skin.js_ - this is essentially the bootstrap file for a skin. It is responsible for loading the CSS for the skin, and contains global overrides for SmartClient component properties that affect the appearance of those components.
*   _skin\_styles.css_ - this file defines the set of CSS classes and styles available for styling the visual elements of SmartClient components
*   _images/_ - this sub-directory typically contains all the icons and other images needed by a skin

Skins are loaded via the `skin` attribute of the [loadISCTag](loadISCTag.md#kb-topic-isomorphicloadisc) or by including the appropriate `load_skin.js` source file with a standard script include tag.

You can create a custom skin with your own look and feel by copying an existing skin and modifying the media, CSS class definitions and component property overrides you wish to change.

Note that the `load_skin.js` file contains a [Page.setSkinDir](../classes/Page.md#classmethod-pagesetskindir) directive to set up the skin dir (used to ensure media is retrieved from the appropriate directory), and a [Page.loadStyleSheet](../classes/Page.md#classmethod-pageloadstylesheet) directive to load the .css file.

See the [Skinning Overview](skinning.md#kb-topic-skinning--theming) for more information.

### Related

- [Page.setSkinDir](../classes/Page.md#classmethod-pagesetskindir)
- [Page.loadStyleSheet](../classes/Page.md#classmethod-pageloadstylesheet)
- [Page.setAddVersionToSkinCSS](../classes/Page.md#classmethod-pagesetaddversiontoskincss)
- [Page.isAddVersionToSkinCSS](../classes/Page.md#classmethod-pageisaddversiontoskincss)

### See Also

- [appearance](appearance.md#kb-topic-appearance)
- [images](images.md#kb-topic-images)
- [files](files.md#kb-topic-files)

---
