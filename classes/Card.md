# Card Documentation

[← Back to API Index](../reference.md)

---

## Class: Card

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
[VLayout](../reference.md#class-vlayout) subclass with rounded corners and subtle shadow (card style). Uses `styleName: "cardPanel"`.

Cards support optional structured content via:

*   [title](#attr-cardtitle): a styled header at the top
*   [cardImage](#attr-cardcardimage): a hero image above the title
*   [showSeparator](#attr-cardshowseparator): a horizontal rule between the title and body content

### Groups

- skinVariant

---
## Attr: Card.showSeparator

### Description
When true and a [title](#attr-cardtitle) is set, a styled horizontal rule is drawn between the title and the body content. Defaults to true when a title is present.

**Flags**: IR

---
## Attr: Card.cardImageMode

### Description
How the [cardImage](#attr-cardcardimage) is displayed:

*   `"hero"` (default): full-width banner at the top of the card, above the title. Top corners are rounded to match the card border radius.
*   `"side"`: fixed-width image on the left; title and body flow vertically on the right. Creates a horizontal layout within the card.
*   `"background"`: image fills the entire card background with a dark gradient overlay so title and body text remain readable.

**Flags**: IR

---
## Attr: Card.title

### Description
Optional title text displayed in a styled header at the top of the card (below the image, if any).

**Flags**: IR

---
## Attr: Card.cardImage

### Description
Optional image displayed in the card. The image placement is controlled by [Card.cardImageMode](#attr-cardcardimagemode).

**Flags**: IR

---
