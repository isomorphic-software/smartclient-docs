# NPMJS Support

[← Back to API Index](../main.md)

---

## KB Topic: NPMJS Support

### Description
SmartClient client-side resources - the JavaScript runtime, skins, and schema - can be installed and updated via [npmjs](https://www.npmjs.com). Select the appropriate package based on your licensing:

*   [smartclient-lgpl](https://www.npmjs.com/package/smartclient-lgpl)
*   [smartclient-eval](https://www.npmjs.com/package/smartclient-eval)
*   [smartclient-pro](https://www.npmjs.com/package/smartclient-pro)
*   [smartclient-power](https://www.npmjs.com/package/smartclient-power)
*   [smartclient-enterprise](https://www.npmjs.com/package/smartclient-enterprise)

**Note:** the SmartClient npm module requires an environment, such as [React](https://en.wikipedia.org/wiki/React_\(JavaScript_library\)) or [Angular](https://en.wikipedia.org/wiki/Angular_\(web_framework\)), that defines "window" as a global with real browser document and navigator objects.

## Installation

**When installing a module in npm v7, console output is suppressed, and interactive output is not allowed. So by default, we now install without prompting wherever a default response is available. Please be patient as it may take a minute or more, depending on your connection and hardware, to finish, with no console updates to indicate progress.**

To install one of these packages, use:

```
   npm install <package name> [flags]
```
where the flags are as follows:

| Option Name | Argument Value | Description |
|---|---|---|
| location | path | A path (absolute or relative to the dependent module) specifying where to install the SmartClient runtime(s). Default is to place the runtime root directory (isomorphic) in the dependent module directory. |
| branch | number | Desired branch (e.g. 11.1). Default is the latest release. |
| date | date in format YYYY-MM-DD \| latest | Desired date. Default is to use the latest build available. |
| runtime | release \| debug \| both | Desired runtime(s) to install. Default is to install them both. |
| reference | true \| false | Whether to keep the framework reference directory. Default is to not install it to save disk space. |
| skins | Tahoe \| all \| none | Which skins (if any) to install. Default is to only install Tahoe. |
| username | string | The username for your SmartClient account. Required for the Pro, Power, and Enterprise packages, and available subject to your licensing. |
| password | string | The password for your SmartClient account. Required for the Pro, Power, and Enterprise packages, and available subject to your licensing. |
| analytics | true \| false | Whether to install the optional [Analytics Module](loadingOptionalModules.md#kb-topic-loading-optional-modules). Only available for the Power, and Enterprise packages, subject to your licensing. |
| rtm | true \| false | Whether to install the optional [RealtimeMessaging Module](loadingOptionalModules.md#kb-topic-loading-optional-modules). Only available for the for the Power, and Enterprise packages, subject to your licensing. |
| prompt | true \| false | Wait for input instead of assuming the default response to all queries during install; default is to not prompt to support newer npm releases. |

After installation, command-line configuration is persisted, so command-line arguments only need to be supplied when updating if the desired configuration has changed. If a username and password aren't supplied via the above options, you will be prompted to enter them by the update script. A password typed in response to the script won't be persisted to your configuration, so you may choose to always enter it interactively for security.

## Updating

Since 'npm update' no longer runs a package's update script if the version hasn't changed, and smartclient npm packages are versioned separately from nightly SDK builds, you must go to the smartclient npm module directory, and run using the syntax
```
   npm run update [flags]
```
to update your installation to the latest runtimes. The supported flags are the same as during installation.

## Using npm v7

The install script for a module is no longer allowed to write output in npm v7, which means that we can no longer interactively query for decisions or show zip download progress. So, to still have a complete install process, the module now proceeds automatically, without waiting, wherever a default response is available for what was formerly an interactive query. Please be patient as the zip download and installation of framework, skins, and other assets may take more than a minute, during which no additional output indicating progress will be printed.

You have a few alternatives to this default behavior:

*   You can pass "--prompt" to "npm install ...". Due to npm v7 rules, installing the module this way will skip the download and installation of the SmartClient framework and skins, and the isc-config.json configuration file won't be created. So afterwards, to install the missing assets you should navigate down to the module directory (under node\_modules) and manually execute "npm run update \[flags\]", passing your install flags.
*   In addition to "--prompt", you can also pass "--foreground-scripts" as a flag to the install command to allow output as in npm v6, but in npm v7 this seems to trigger other timing logs that obfuscate what we print. Hopefully, support for the "--foreground-scripts" flag will improve in future npm releases.

Note that since there are no default responses for the "username" and "password" flags, if they are required, installation of assets will be skipped (as in the first bullet above) unless you provide bindings on the command line initially for "npm install ...".

"Uninstall" is no longer a lifecycle event in npm v7, so a module's uninstall script declared in package.json no longer gets called during uninstallation. The recommended workaround is to run "npm run uninstall" from the module directory (under node\_modules) before uninstalling.

## Examples

New install of SmartClient Evaluation, selecting a specific branch and date:
```
   npm install smartclient-eval --branch=11.1 --date=2018-12-30
```
Update to latest nighlty build (run from package directory):
```
   npm run update --date=latest
```
Update to SmartClient 12.1 branch, installing all skins:
```
   npm run update --branch=12.1 --skins=all
```

## Importing

If you are building a new Angular, React or similar application, and plan to use SmartClient pervasively throughout, you can just add an import declaration to your `main.ts` or `App.tsx` to make the framework available. However, if you are adding SmartClient to an existing application, and you only plan to use SmartClient for specific components like grids, or for [Reify screens](reifyForDevelopers.md#kb-topic-reify-for-developers), consider using [background download](backgroundDownload.md#kb-topic-background-download) instead of importing SmartClient directly (importing causes SmartClient to load immediately on all pages).

To directly import the release or debug framework, respectively, in your application, you can write:

```
   import 'smartclient-eval/debug';
```
or
```
   import 'smartclient-eval/release';
```
To import a skin as well, such as "Tahoe", you can add:
```
   import 'smartclient-eval/skins/Tahoe';
```
To import one of the optional modules, you'd write something like:
```
   import 'smartclient-eval/debug/rtm';
```
or
```
   import 'smartclient-eval/release/analytics';
```
respectively, to import the debug version of the Realtime Messaging module or the release version of the Analytics module.

**Caution:** you can't mix debug and release imports in a single app.

#### Importing skins in Angular
In Angular, if you directly import the skin, you may need to manually add the path to the `skin_styles.css` file for your skin to the `src/styles.css` file (or equivalent) for your app, in addition to importing the skin as described above.

For example, if you've installed the SmartClient runtime in the default location, and are importing Tahoe, you'd add the following to `src/style.css` in your app:

```
   @import '../isomorphic/skins/Tahoe/skin_styles.css';
```
**Note:** if you are using the [FileLoader](../main_2.md#object-fileloader) to load a skin, it must be installed under `src/assets` (for example copied from `isomorphic/skins`) to work properly.
#### Using SmartClient APIs
If you want to refer to SmartClient APIs through your own constant, you can always issue a declaration such as:
```
   const ISC: typeof isc = window['isc'];
```
after importing this package.

## TypeScript

To provide typescript support, the installation process should automatically augment your `tsconfig.json` file with an include directive targeting SmartClient's typescript file.

Alternatively, you can copy the typescript declaration file, `smartclient.d.ts`, from the installed resources under the `isomorphic` directory to your app's source directory, and then import it from your app like:

```
   import 'smartclient.d.ts';
```
SmartClient's TypeScript support is intended for IDE auto-completion and inline documentation, not for transpilation. So, if you run into compile errors, you can always remove any reference to our TypeScript file from your own TS file and application, remove `smartclient.d.ts` from under `src/assets` (if present), and instead make TypeScript active for your IDE only. For further details, see the TypeScript support documentation for [our framework](typeScriptSupport.md#kb-topic-typescript-support) or your IDE.

### See Also

- [iscInstall](iscInstall.md#kb-topic-installing-the-smartclient-runtime)

---
