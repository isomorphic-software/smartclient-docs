# Customizing Skins

[← Back to API Index](../reference.md)

---

## KB Topic: Customizing Skins

### Description
A skin gives a SmartClient application its look and feel. On disk, a skin is a directory the framework loads, made up of three parts:

*   `skin_styles.css` - the stylesheet.
*   `load_skin.js` - loads the stylesheet and the skin's fonts, and applies the skin's widget defaults (scrollbars, icon sizing, spacing and so on).
*   `images/` - the skin's image assets.

For the general picture of how SmartClient components are styled, see [skinning](skinning.md#kb-topic-skinning--theming). This discussion covers creating and customizing SmartClient's _modern_ skins.

#### Modern skins
SmartClient's modern skins - the "Flat" series, such as Tahoe, Shiva and Stratus - were built with Sass in earlier releases. They no longer are: they are free of that toolchain, and use a purely CSS-and-JSON approach.

That approach has three parts:

*   styling is driven by CSS custom properties, `var(--isc-*)`;
*   a skin is edited as data - a single JSON file, `config.json`;
*   the built `skin_styles.css` and `load_skin.js` are _tokenized_: they carry marked regions that the framework fills from `config.json` - the variable values, plus any custom CSS, fonts and JavaScript.

A modern skin's whole appearance therefore comes down to the values in its `config.json`. You edit that file, and `skin_styles.css` is produced from it; you never edit `skin_styles.css` by hand.

A modern skin also normally _derives_ from another. It names a `baseSkin` and records only the variables - and any custom CSS, fonts or JavaScript - that it changes. This keeps skins small, and lets a skin inherit later improvements to the one it was built on.

(Some older skins, such as the Enterprise series, are still generated from Sass templates, and are customized differently.)

#### The config.json format
A skin's `config.json` is a single object. A minimal one names the skin, names the base it derives from, and lists the variables it changes:
```
 {
     "name": "MyTheme",
     "baseSkin": "Tahoe",
     "settings": {
         "--isc-highlight_color": "#40BF41",
         "--isc-standard_button_border_radius": "5px"
     }
 }
 
```

The top-level fields are:

**`name`**  
The skin's name. Matches its directory.

**`baseSkin`**  
The skin this one derives from. A base skin is its own base.

**`settings`**  
An object mapping `--isc-*` variables to their values: colors, fonts, sizes, corner radii and so on. You list only the variables you want to change from the base skin. This is the bulk of most skins; see "Variables and the cascade" below.

**`useLiveCSS`**  
Whether the skin is served live (`true`, the default) or as a frozen snapshot. See "Deploying a skin" below.

**`customCSS`, `customJS`, `customSVG`, `fontCss`**  
The skin's own custom CSS, JavaScript, stock-icon SVG symbols and `@font-face` declarations, held inline. See "Custom CSS, fonts and JavaScript" below.

**`customCSSFile`, `customJSFile`, `customSVGFile`, `fontCssFile`**  
A file alternative to each field above. Instead of inline content, the field holds the name of a sibling file in the skin's directory. A value is stored _either_ inline _or_ as a file reference, never both.

**`fontList`**  
The fonts the skin uses, so the framework can load them.

**`density`**  
The skin's spacing density.

**`version`**  
A counter, bumped each time the skin is saved.

#### Variables and the cascade
A skin is driven entirely by CSS custom properties, so a few high-level changes can restyle the whole framework.

Most of a skin's look derives from a small set of "primary" variables. For example, `--isc-highlight_color` sets the accent color used across buttons, headers, selection and focus.

Variables can be defined in terms of one another, and can use CSS color math such as `oklch()` and `color-mix()`. A single edit can therefore retune an entire palette while preserving its contrast and tint relationships.

The complete list of variables lives in any skin's `config.json`, or in the `:root{}` block of its `skin_styles.css`. The Skin Editor presents the same variables organized by component and role, with a live preview.

#### Custom CSS, fonts and JavaScript
Beyond variable values, a skin can carry its own custom CSS, `@font-face` declarations and JavaScript. These live in the `customCSS`, `fontCss` and `customJS` fields - inline, or in sibling files via their `...File` counterparts.

The framework merges them into the skin, keeping a base skin's own custom styles separate from those a derived skin adds. Customizing a skin therefore never discards the styling it inherited.

#### Compact skins
If your application runs on the SmartClient server, a skin can take a more compact form.

In place of the three files above, the skin's directory holds a single `.skin.json` file. The server expands it into a working skin on the fly, overlaying the skin's config onto its base skin and serving the result.

Because the server does this on every request, a compact skin is served _live_: it always reflects the current version of the base skin it derives from.

A `.skin.json` is written as an `isc_userSkin` record. The record serves only to identify the skin - its outer `name` and `baseSkin` - and to hold the skin's config in a `userSettings` field. That `userSettings` object is exactly the `config.json` content described above.

For example, a purple variant of Shiva is a directory `skins/PurpleShiva` holding one file, `PurpleShiva.skin.json`:

```
 {
     "name": "PurpleShiva",
     "baseSkin": "Shiva",
     "userSettings": {
         "name": "PurpleShiva",
         "baseSkin": "Shiva",
         "useLiveCSS": true,
         "settings": { "--isc-highlight_color": "purple" }
     }
 }
 
```

Load any page with `skin=PurpleShiva` in the URL - for example the Feature Explorer at `/showcase/?skin=PurpleShiva`. The server serves it as though it were a base skin, with your highlight color applied everywhere it cascades.

#### Creating a skin
#### With the Skin Editor
The [Skin Editor](skinEditor.md#kb-topic-skin-editor) is the easiest way to create and customize a skin. It manages the skin's config for you, editing its variables and custom CSS, fonts and JavaScript with a live preview.

It is available online, or in your own environment with a [Pro or better](https://www.smartclient.com/product/) license.

When a skin is stored in a DataSource and the Skin Editor runs on the same server as your application, your changes take effect immediately - the skin does not have to be exported.

#### By hand, as a compact skin
A compact skin (above) is the simplest skin to write by hand. Create the skin's directory, add a `.skin.json` naming a base skin and the settings you want to change, and load the page with `skin=_YourSkin_`.
#### As a full skin directory
For a self-contained skin with its own stylesheet and assets, copy an existing skin's directory. For example, copy `skins/Tahoe` to `skins/MySkin`, replace "Tahoe" with "MySkin" in `load_skin.js`, and edit `MySkin`'s `config.json`.
#### Deploying a skin
#### With the SmartClient server
Deploy the skin's `config.json` (or its `.skin.json` record), and the server produces `skin_styles.css` on demand.

By default this is the live overlay described above. You can instead _freeze_ a skin (`useLiveCSS:false`): the server then serves a baked, self-contained snapshot that no longer tracks its base. Freezing is useful when you want a skin's appearance pinned.

#### On a static web server
To host a skin with no SmartClient server at all, deploy a built `skin_styles.css`. Each skin ships with a small command-line build that regenerates it from `config.json`, with no server and no Sass toolchain.

---
