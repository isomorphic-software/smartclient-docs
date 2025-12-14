# skins

[← Back to API Index](../reference.md)

---

## KB Topic: skins

### Description
Properties used to manage to the the overall appearance of the application.

A "skin" consists of

*   `skin_styles.css`: a .css file defining the set of classes to apply to SmartClient components' visual elements
*   `images/`: a directory of image files used as part of visual components
*   `load_skin.js`: a .js file containing overrides for various SmartClient component properties that affect the appearance of those components.

Skins are loaded via the `skin` attribute of the [loadISCTag](loadISCTag.md#kb-topic-isomorphicloadisc) or by including the appropriate `load_skin.js` source file with a standard script include tag.

To create a custom skin, we suggest making a complete copy of an existing skin, then modifying the media, css class definitions and component property overrides you wish to change.

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
