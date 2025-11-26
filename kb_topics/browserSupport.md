# Supported Browsers

[← Back to API Index](../reference.md)

---

## KB Topic: Supported Browsers

### Description
When considering which browser versions are supported, developers should consider which browser versions they wish to support within their application. Generally this will be a subset of what the framework supports, and should be decided based on the needs of your customers (typically corporate policies on browser usage for intranet applications, or general browser usage for customer facing applications).

The SmartClient framework supports all major browsers, and will always support the current versions at release-time.

The full list of SmartClient browser support (at the time of the initial ${version} release) is listed below. Note that support for some framework features may be implemented using different native approaches - or in rare cases, may be unavailable - in some older browser versions. Such cases are covered in documentation where they occur. For example, see the [skinning](skinning.md#kb-topic-skinning--theming) discussion about CSS3 mode.

At the application level, we'd typically recommend advertising support for the latest versions of Chrome, Safari and Firefox, the most recent Firefox ESR release and the most common (and most recent) versions of Internet Explorer.

#### Support for new browser versions introduced after SmartClient release
When new browser versions are released we will generally determine whether any issues are introduced by the new version, and update the most recent released SmartClient version to add support for these new browsers if changes are necessary. These changes will be made available in nightly patch builds.

Older branches of SmartClient may also be updated to support new browser versions. This will be considered on a case-by-case basis, depending on the effort required to work around any newly introduced browser bugs on these older branches.

#### Unsupported browser handling
Every distributed SmartClient skin contains an "Unsupported Browser" page. This is an optional placeholder for an application to state its browser support policies.

**The following browser versions were supported as of the original ${version} release**:

|  | Browser/Version | Operating System(s) |
|---|---|---|
|  | Edge ${Edge_versions} | ${Edge_platforms} |
|  | Firefox ${Firefox_versions} | ${Firefox_platforms} |
|  | Safari ${Safari_versions} | ${Safari_platforms} |
|  | Chrome ${Chrome_versions} | ${Chrome_platforms} |
|  | Opera ${Opera_versions} | ${Opera_platforms} |
|  | Safari (mobile) | ${Safari_mobile_platforms} |
|  | Android browser | ${Android_mobile_platforms} |

### Related

- [Page.checkBrowserAndRedirect](../classes/Page.md#classmethod-pagecheckbrowserandredirect)
- [Page.getUnsupportedBrowserPromptString](../classes/Page.md#classmethod-pagegetunsupportedbrowserpromptstring)
- [Page.defaultUnsupportedBrowserURL](../classes/Page.md#classattr-pagedefaultunsupportedbrowserurl)
- [Page.unsupportedBrowserAction](../classes/Page.md#classattr-pageunsupportedbrowseraction)

---
