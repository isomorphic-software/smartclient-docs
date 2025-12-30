# Customizing Sass-based Skins

[← Back to API Index](../reference.md)

---

## KB Topic: Customizing Sass-based Skins

### Description
#### Skin Editor
To create new skins and easily make bulk changes to details like colors and fonts, see our [Skin Editor](skinEditor.md#kb-topic-skin-editor) tool, which can be accessed online, or locally in your environment if you have a [Pro or better](https://www.smartclient.com/product/) license.
#### Support for templated skins
Some skins have a stylesheet generated from [Sass templates](https://sass-lang.com/install) and compiled with [compass](http://compass-style.org/). Each such skin has a "template" subdirectory containing various files, including those used to regenerate the skin's stylesheet (skin\_styles.css) using `compass`. The files of interest to a custom skin are in the template/sass directory:
#### Files you can edit

*   \_userSettings.scss - This file is initially empty and can be edited. It should contain Sass variables and font declarations intended to override settings in the builtin skin (see `_skinSettings.scss` and `_base.scss` below)
*   \_userStyles.scss - This file is initially empty and can be edited. It should contain CSS intended to be incorporated after the styles in the builtin skin (see `_skinStyles.scss` and `_base.scss` below), overriding both

#### Files that should not be edited
The other files in template/sass should not be edited and can be largely ignored (see the discussion below on _Keeping the skin you extended up to date_) - but their purpose is listed here:

*   skin\_styles.scss - This is the bootstrap file that lists the fragments to load and is executed by running 'compass compile' in the parent folder. There shouldn't be any need to alter this file - but you can do so if you want to add further custom fragments
*   \_base.scss - This file contains all the base CSS and the defaults for the supported variables in the builtin skin that your custom skin is based on. This file should not be edited
*   \_skinSettings.scss - This file contains Sass variables and font-declarations for the builtin skin, intended to override the defaults set up in \_base.scss. This file should not be edited
*   \_skinStyles.scss - This file contains custom CSS for the builtin skin, to be appended after that in \_base.scss. This file should not be edited

#### Creating a custom skin
A custom skin is created by copying and extending an existing one.

You can start from whichever templated skin is closest to your requirement. Variable values largely cascade from one another, allowing simple, high-level changes to affect much of the skin.

To create a custom skin based on "Tahoe":

*   Copy the skins/Tahoe directory to skins/MySkin
*   In skins/MySkin/load\_skin.js, find and replace instances of "Tahoe" with "MySkin"
*   In skins/MySkin/template/sass/\_userSettings.scss, declare $theme\_name: 'MySkin'
*   Change to skins/MySkin/template and run 'compass compile'

#### Customizing your skin
#### What to edit

As noted at the top of this discussion, the files you can edit are in the template/sass directory - specifically, `_userSettings.scss` for customizing supported variable values and `_userStyles.scss`, for overriding existing styles.

You can see the CSS classes that can be overridden in `_base.scss`.

You can see the list of available variables in `_skinSettings.scss`, grouped and named according to what effects they have. You can copy the variables you want to override into your `_userSettings.scss` file, change their values and run 'compass compile'.

#### By way of example
To create a generally green version of Tahoe, try adding these settings to `_userSettings.scss` and running 'compass compile'

$highlight\_color: #40BF41; // generally green rather than blue  
$standard\_widget\_border\_color: #006400; // darkgreen borders for widgets  
$standard\_button\_border\_radius: 5px; // give all buttons rounded corners  

#### After editing
When you make changes to `_userSettings.scss` or `_userStyles.scss`, you can compile them into your skin by running 'compass compile' from the skins/MySkin/template directory. This compiles the various fragments from the template/sass directory (listed in `skin_styles.scss`) to produce the skin's stylesheet, at skins/MySkin/skin\_styles.css.

After making changes and running 'compass compile', clear your browser cache before refreshing your test page, to ensure the old skin\_styles.css isn't cached.

#### Keeping the skin you extended up to date
As noted earlier, some of the files in template/sass should not be edited. This is because, from time to time, we may make fixes or improvements to our builtin skins - when this happens, you can keep your custom skins up to date, without clobbering any of your customizations, by copying `_base.scss`, `_skinSettings.scss` and `_skinStyles.scss` from the skin you extended to your skin's template/sass folder, replacing the existing copies. From there, running 'compass compile' will incorporate the latest builtin skin changes into your custom skin, without affecting your existing customizations.

---
