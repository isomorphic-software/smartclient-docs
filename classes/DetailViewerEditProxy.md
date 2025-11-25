# DetailViewerEditProxy Documentation

[← Back to API Index](../main.md)

---

## Class: DetailViewerEditProxy

*Inherits from:* [CanvasEditProxy](../main.md#class-canvaseditproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [DetailViewer](DetailViewer.md#class-detailviewer) components when editMode is enabled.

### Groups

- devTools

---
## Attr: DetailViewerEditProxy.dataEscapeChar

### Description
If [inline editing](EditProxy.md#attr-editproxyinlineeditevent) for this viewer edits the [DetailViewer.data](DetailViewer.md#attr-detailviewerdata), character that can be used to enter literal separator chars (such as the [dataSeparatorChar](#attr-detailviewereditproxydataseparatorchar)) or literal leading or trailing whitespace.

Repeat this character twice to enter it literally. For example, with the default of "\\", inputting "\\\\" would result in a literal backslash in the value.

**Flags**: IR

---
## Attr: DetailViewerEditProxy.dataDisplaySeparatorChar

### Description
If [inline editing](EditProxy.md#attr-editproxyinlineeditevent) for this viewer edits the [DetailViewer.data](DetailViewer.md#attr-detailviewerdata), character that should be used as a separator for entering [ValueMap](../main_2.md#type-valuemap)-style entries that map from a field name to a value.

With the default of ":", the following input:

```
      1:Fixed, 2:Won't Fix, 3:Resolved
 
```
Would be assumed to be a mapping like this (expressed in JSON):
```
   {
      "1" : "Fixed",
      "2" : "Won't Fix",
      "3" : "Resolved"
   }
 
```

Any entry without a separator char has an implied value of `null`. For example, for this input:

```
       Fixed:Reported Fixed, WontFix:Won't Fix, Resolved
 
```
The resulting `data` would be:
```
   {
      "Fixed" : "Reported Fixed",
      "WontFix" : "Won't Fix",
      "Resolved" : null
   }
 
```

The [dataEscapeChar](#attr-detailviewereditproxydataescapechar) can be used to enter literal colon characters.

Set `dataDisplaySeparatorChar` to null to prevent entry of values - user input will always be treated as just a list of legal field names.

**Flags**: IR

---
## Attr: DetailViewerEditProxy.dataSeparatorChar

### Description
If [inline editing](EditProxy.md#attr-editproxyinlineeditevent) for this viewer edits the [DetailViewer.data](DetailViewer.md#attr-detailviewerdata), character that should be used as a separator between values, or between pairs of field name vs values if the user is entering such a [ValueMap](../main_2.md#type-valuemap) using the [dataDisplaySeparatorChar](#attr-detailviewereditproxydatadisplayseparatorchar).

If [EditProxy.inlineEditMultiline](EditProxy.md#attr-editproxyinlineeditmultiline) is enabled, newlines will be used as value separators and the `dataSeparatorChar`

The [dataEscapeChar](#attr-detailviewereditproxydataescapechar) can be used to enter the separator char as part of a field name or value.

**Flags**: IR

---
## Method: DetailViewerEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the component's `data` and `fields`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new component data |

---
## Method: DetailViewerEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the component's data one-field-per-line as specified in [DetailViewerEditProxy.dataDisplaySeparatorChar](#attr-detailviewereditproxydatadisplayseparatorchar).

---
