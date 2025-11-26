# FontLoader Documentation

[← Back to API Index](../reference.md)

---

## Class: FontLoader

### Description
Force-loads the custom fonts declared in the ${isc.DocUtils.linkForRef('group:skinning','current skin\\'s CSS file')} and updates any potentially-affected, already-drawn canvii when loading completes. Without FontLoader, auto-sized canvii that use custom fonts may end up with the wrong size if a page is loaded when its custom fonts are not available in the browser cache.

To disable FontLoader, set  `window.isc_loadCustomFonts = false`  before SmartClient is loaded.

If you want to avoid the Framework redrawing canvii after the fonts load, you may want to code your app to delay drawing anything until the skin fonts are loaded. You can check [FontLoader.isLoadingComplete](#classmethod-fontloaderisloadingcomplete) to see whether loading is done, and if it's not, you can set a "fontsLoaded" [page event](Page.md#classmethod-pagesetevent) to run code when it's done or a "fontLoadingFailed" [page event](Page.md#classmethod-pagesetevent) to run code if there's an error.

#### Advanced Usage
`FontLoader` will use the new [CSS Font Loading API](https://developer.mozilla.org/en-US/docs/Web/API/CSS_Font_Loading_API) in browsers in which it's available and has proven reliable. Otherwise, we fall back to canvas measurement techniques to detect loading. To force fallback and avoid the API, set  `window.isc_useCSSFontAPI = false` , or to force the API to be used (where it exists but may be unreliable) set  `window.isc_useCSSFontAPI = true` , before SmartClient is loaded.

If you're loading additional style sheets, beyond the skin, that declare custom fonts with @font-face, you can request that the `FontLoader` force-load them as well by specifying them in `window.isc_additionalFonts` as an array of the font family names matching those from the @font-face declarations.

Note that currently, if you have more than one font with the same font family name in your CSS, you'll need to use the CSS Font Loading API approach if you want them all loaded by the FontLoader. Under the measurement approach, the FontLoader is only able to load the default font for each font family, since it has no knowledge beyond the specified family names.

---
## ClassMethod: FontLoader.isLoadingComplete

### Description
Whether all requested custom fonts have been loaded. If this method returns true, you know that the [FontLoader](#class-fontloader) won't need to redraw any canvii drawn afterwards, and that a "fontsLoaded" or "fontLoadingFailed" [page event](Page.md#classmethod-pagesetevent) won't fire (it may have previously fired).

### Returns

`[boolean](../reference.md#type-boolean)` — whether all requested fonts have been loaded

---
