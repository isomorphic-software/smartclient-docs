# Customizing Sass-based Skins

[← Back to API Index](../reference.md)

---

## KB Topic: Customizing Sass-based Skins

### Description
#### Skin Editor
To create new skins and easily make bulk changes to details like colors and fonts, see our [Skin Editor](skinEditor.md#kb-topic-skin-editor) tool, which can be accessed online, or locally in your environment if you have a [Pro or better](https://www.smartclient.com/product/) license.
#### Support for templated skins
Some skins have a stylesheet generated from [Sass templates](https://sass-lang.com/install) and compiled with [compass](http://compass-style.org/). Each such skin has a "template" subdirectory containing various files, including those used to regenerate the skin's stylesheet (skin\_styles.css) using `compass`. The files of interest to a custom skin are in the template/sass directory:

*   skin\_styles.scss - This is the bootstrap SASS file that lists the fragments to compile into your custom skin, and is executed by running 'compile' in the parent folder. There shouldn't be any need to alter this file - but you can do so if you want to add further custom fragments
*   \_base.scss - This file contains the variable-defaults and base CSS for the skin that your custom skin is based on. Note that @font-face definitions are declared in a separate `_fonts.scss` file. See below. This file should not be edited.

#### Files you can edit

*   \_fonts.scss - This file defines the CSS @font-faces to load for this skin and can be edited. This content is the only base-skin CSS that isn't in `_base.scss`, kept separate so custom skins can have different fonts, without leaving orphaned font-loads in `_base.scss`.
*   \_userSettings.scss - This file is initially empty and can be edited. It should contain Sass variables intended to override settings in the builtin skin (see `_base.scss` below)
*   \_userStyles.scss - This file is initially empty and can be edited. It should contain CSS styles intended as overrides, to be incorporated after the styles in the builtin skin (see `_base.scss` below).

#### Creating a custom skin
A custom skin is created by copying and extending an existing one.

You can start from whichever templated skin is closest to your requirement. Variable values largely cascade from one another, allowing simple, high-level changes to affect much of the skin.

To create a custom skin based on "Tahoe":

*   Copy the skins/Tahoe directory to skins/MySkin
*   In skins/MySkin/load\_skin.js, find and replace instances of "Tahoe" with "MySkin"
*   In skins/MySkin/template/sass/\_userSettings.scss, declare $theme\_name: 'MySkin'
*   Change to skins/MySkin/template and run 'compile'

#### Customizing your skin
#### What to edit

As noted at the top of this discussion, the files you can edit are in the template/sass directory - specifically, `_userSettings.scss` for customizing supported variable values, `_userStyles.scss`, for overriding existing styles or adding new ones, and `_fonts.scss` for changing the fonts.

You can see the CSS classes that can be overridden in `_base.scss`.

You can also see the list of available variables in that file, grouped and named according to what effects they have. You can copy the variables you want to override into your `_userSettings.scss` file, change their values and run 'compile' from the parent directory.

#### By way of example
To create a generally green version of Tahoe, try adding these settings to `_userSettings.scss` and running 'compile' from the parent directory

$highlight\_color: #40BF41; // generally green rather than blue  
$standard\_widget\_border\_color: #006400; // darkgreen borders for widgets  
$standard\_button\_border\_radius: 5px; // give all buttons rounded corners  

#### After editing
When you make changes to `_userSettings.scss` or `_userStyles.scss`, you can compile them into your skin by running 'compile' from the skins/MySkin/template directory. This compiles the various fragments from the template/sass directory (listed in `skin_styles.scss`) to produce the skin's stylesheet, at skins/MySkin/skin\_styles.css.

After making changes and running 'compile', clear your browser cache before refreshing your test page, to ensure the old skin\_styles.css isn't cached.

#### Keeping the skin you extended up to date
As noted earlier, some of the files in template/sass should not be edited. This is because, from time to time, we may make fixes or improvements to our builtin skins - when this happens, you can keep your custom skins up to date, without clobbering any of your customizations, by copying `_base.scss` from the skin you extended to your skin's template/sass directory, replacing the existing copy. If you haven't customized your fonts, you can copy `_fonts.scss` as well, which will include any internal font changes we make. From there, running 'compile' will incorporate the latest builtin skin changes into your custom skin, without affecting your existing customizations.

Note - compass will fail to compile if it thinks there are no changes to include, and this can happen for various reasons. To work around this, the 'compile' batch files in the template directory pass the `--force` switch to compass, to ensure it always recompiles. Additionally, when compass runs, it creates a hidden directory, called sass-cache, in the skin's template structure - this can be safely removed, and should always be removed if any compilation issues arise.

---
