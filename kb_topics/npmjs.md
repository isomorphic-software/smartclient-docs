# NPMJS Support

[← Back to API Index](../reference.md)

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
| yes | true \| false | Assume answer 'yes' to prompts with default. This allows the install or update process to complete without interaction, to enable complete automation. |

After installation, command-line configuration is persisted, so command-line arguments only need to be supplied when updating if the desired configuration has changed. If a username and password aren't supplied via the above options, you will be prompted to enter them by the update script. A password typed in response to the script won't be persisted to your configuration, so you may choose to always enter it interactively for security.

## Updating

Since 'npm update' no longer runs a package's update script if the version hasn't changed, and smartclient npm packages are versioned separately from nightly SDK builds, you must go to the smartclient npm module directory, and run using the syntax
```
   npm run update [flags]
```
to update your installation to the latest runtimes. The supported flags are the same as during installation.

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

If you are building a new Angular, React or similar application, and plan to use SmartClient pervasively throughout, you can just add an import declaration to your `main.ts` or `App.tsx` to make the framework available. However, if you are adding SmartClient to an existing application, and you only plan to use SmartClient for specific components like grids, or for [Reify screens](reifyForDevelopers.md#kb-topic-reify-for-developers), consider using [background download](#kb-topic-backgrounddownload) instead of importing SmartClient directly (importing causes SmartClient to load immediately on all pages).

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
**Note:** if you are using the [FileLoader](../reference_2.md#object-fileloader) to load a skin, it must be installed under `src/assets` (for example copied from `isomorphic/skins`) to work properly.
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

- [iscInstall](iscInstall.md#kb-topic-deploying-smartclient)

---
