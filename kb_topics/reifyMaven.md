# Importing from Reify

[← Back to API Index](../main.md)

---

## KB Topic: Importing from Reify

### Description
SmartClient [support for Maven](mavenSupport.md#kb-topic-maven-support) includes the ability to [import](http://github.smartclient.com/isc-maven-plugin/reify-import-mojo.html) (and optionally, [verify](http://github.smartclient.com/isc-maven-plugin/reify-validate-mojo.html) ) assets from [reify.com](http://reify.com) into your project either on-demand or during your build process. Using the [example configuration](http://github.smartclient.com/isc-maven-plugin/examples/configuration.html), the import command might look something like the following:

```
   mvn com.isomorphic:isc-maven-plugin:1.4.5:reify-import -Pisc
 
```
**Important:** This flow is unidirectional. That is, whatever changes are to be made to these resources should be made using the collaborative Reify environment and then re-imported. There is, by design, no reason to modify them locally, and the plugin takes steps to notify you when that happens. Refer to the [Reify for Developers](reifyForDevelopers.md#kb-topic-reify-for-developers) documentation topic for further discussion.

---
