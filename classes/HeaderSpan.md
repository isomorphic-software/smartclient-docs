# HeaderSpan Documentation

[← Back to API Index](../reference.md)

---

## Attr: HeaderSpan.title

### Description
A title for this headerSpan, to display in the headerSpan button for this headerSpan and in other contexts such as the [menu for picking visible fields](ListGrid_1.md#attr-listgridcanpickfields). Note: if you want to use HTML tags to affect the display of the header, you should do so via [HeaderSpan.headerTitle](#attr-headerspanheadertitle) instead so that other places where the title appears in the UI are not affected. Refer to discussion at [ListGridField.title](ListGridField.md#attr-listgridfieldtitle).

### Groups

- headerSpan

**Flags**: IR

---
## Attr: HeaderSpan.wrap

### Description
Should the span title wrap if there is not enough space horizontally to accommodate it. If unset, default behavior is derived from [ListGrid.wrapHeaderSpanTitles](ListGrid_1.md#attr-listgridwrapheaderspantitles). (This is a soft-wrap - if set the title will wrap at word boundaries.)

### See Also

- [ListGridField.wrap](ListGridField.md#attr-listgridfieldwrap)

**Flags**: IR

---
## Attr: HeaderSpan.spans

### Description
This property allows developer to "nest" header spans, grouping fields together by multiple layers of granularity.

For example a group of fields could be nested within two layers of header spans as follows:

```
 { title:"Europe", spans:[
      {title:"France", fields:["Paris", "Lyon"]},
      {title:"UK", fields:["London", "Glasgow"]},
      {title:"Spain", fields:["Barcelona"]}
  ]
 }
 
```
Note that a span definition can not include both `spans` and [fields](#attr-headerspanfields).

### Groups

- headerSpan

**Flags**: IR

---
## Attr: HeaderSpan.height

### Description
Height of this headerSpan. Defaults to [ListGrid.headerSpanHeight](ListGrid_1.md#attr-listgridheaderspanheight).

### Groups

- headerSpan

**Flags**: IR

---
## Attr: HeaderSpan.headerBaseStyle

### Description
Custom base style to apply to the header button created for this span instead of [ListGrid.headerBaseStyle](ListGrid_1.md#attr-listgridheaderbasestyle).

Note that depending on the header button constructor, you may have to specify [HeaderSpan.headerTitleStyle](#attr-headerspanheadertitlestyle) as well.

### Groups

- appearance

**Flags**: IRW

---
## Attr: HeaderSpan.headerTitleStyle

### Description
Custom titleStyle to apply to the header button created for this span instead of [ListGrid.headerTitleStyle](ListGrid_1.md#attr-listgridheadertitlestyle).

Note that this will typically only have an effect if [ListGrid.headerButtonConstructor](ListGrid_1.md#attr-listgridheaderbuttonconstructor) is set to [StretchImgButton](StretchImgButton.md#class-stretchimgbutton) or a subclass thereof.

### Groups

- appearance

### See Also

- [HeaderSpan.headerBaseStyle](#attr-headerspanheaderbasestyle)

**Flags**: IRW

---
## Attr: HeaderSpan.valign

### Description
Vertical alignment of the title of this headerSpan.

Defaults to listGrid.headerSpanVAlign if unset.

### Groups

- headerSpan

**Flags**: IR

---
## Attr: HeaderSpan.align

### Description
Horizontal alignment of the title of this headerSpan.

### Groups

- headerSpan

**Flags**: IR

---
## Attr: HeaderSpan.name

### Description
Name for this headerSpan, for use in APIs like [ListGrid.setHeaderSpanTitle](ListGrid_2.md#method-listgridsetheaderspantitle).

Name is optional, but if specified, must be unique for this ListGrid (but not globally unique) as well as a valid JavaScript identifier, as specified by ECMA-262 Section 7.6 (the [String.isValidID](String.md#staticmethod-stringisvalidid) function can be used to test whether a name is a valid JavaScript identifier).

### Groups

- headerSpan

**Flags**: IR

---
## Attr: HeaderSpan.fields

### Description
List of fields that this header spans. Fields should be identified by their value for [ListGridField.name](ListGridField.md#attr-listgridfieldname).

Developers may define multiple levels of header-spans by specifying [HeaderSpan.spans](#attr-headerspanspans) however a span cannot be specified with both `fields` and `spans`.

### Groups

- headerSpan

**Flags**: IR

---
## Attr: HeaderSpan.headerTitle

### Description
Optional title for the headerSpan button for this headerSpan. If specified this will be displayed in the headerSpan button instead of [HeaderSpan.title](#attr-headerspantitle). Set to an empty string to suppress the title in the header button entirely.

### Groups

- headerSpan

**Flags**: IR

---
