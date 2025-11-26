# Don't Misuse Frames

[← Back to API Index](../reference.md)

---

## KB Topic: Don't Misuse Frames

### Description
Loading the SmartClient framework into multiple frames or iframes within the same browser is not a supported configuration, or more accurately, not a _supportable_ configuration, for the following reasons:

*   each additional frame multiplies the memory footprint and reduces speed
*   having multiple frames prevents drag and drop between components in different frames
*   modality handling (eg modal dialogs) doesn't automatically take into account multiple frames (consider tabbing order, nested modality and other issues, you'll see it's not realistic to provide automatic cross-frame modality handling)
*   inter-frame communication triggers several browser bugs: memory leaks, performance issues, intermittent crashes in some browsers, inconsistencies in basic JavaScript operators such as "typeof", and problems with form focus handling in IE, among many other bugs

None of these problems are specific to SmartClient. They happen with Ajax frameworks in general as well as other RIA technologies. This is why no successful Ajax application has ever used the approach of double-loading a component framework into multiple frames.

The recommended [SmartClient Architecture](smartArchitecture.md#kb-topic-smartclient-architecture) involves loading as many SmartClient-based application views as possible in the first page load, then showing and hiding different views as the user navigates through the application.

If, for whatever reason, you cannot follow the SmartClient Architecture and must load new SmartClient-based views by contacting the server each time, use the [ViewLoader](../classes/ViewLoader.md#class-viewloader) class to load new views, never frames.

Note that the use of IFrames is appropriate in certain circumstances, including loading certain types of content within an [contentsType,HTMLFlow](../classes/HTMLFlow.md#class-htmlflow). The only prohibited usage is loading the SmartClient framework into multiple frames within the same browser.

---
