# Logging migration

[← Back to API Index](../reference.md)

---

## KB Topic: Logging migration

### Description
In Smartclient version 13.1 and later Apache Log4j 2.x is used for [serverLogging](serverLogging.md#kb-topic-server-logging). See the recommendations below on how to migrate to the new logging system.
#### Migrate from Log4j 1.x used directly
If you were using Log4j 1.x directly, you should take any custom settings you want to retain from _log4j.isc.config.xml_ Log4j 1.x configuration file (old) and move them over to _log4j2.isc.config.xml_ Log4j 2.x configuration file (new) according to the Apache's [Migrating from Log4j 1.x to 2.x](https://logging.apache.org/log4j/2.x/manual/migration.html) guide.
#### Migrate from logging system used over the Slf4j bridge
If you were using logging system over the Slf4j bridge, you may switch to the Log4j 2.x API instead as it is now separated from the implementation, so Log4j 2.x may be used as a bridge to other logging systems, including Slf4j.
#### Continue using Log4j 1.x
If you are forced to continue to use Log4j 1.x, you may redirect Smartclient loggin to Slf4j as described in [Redirecting logging to Slf4j framework](serverLogging.md#kb-topic-server-logging) with the Slf4j to Log4j 1.x bridge, or use the default Smartclient Log4j 2.x logging and pass it to the Slf4j by using the [Log4j 2.x to Slf4j adapter](https://logging.apache.org/log4j/2.x/log4j-to-slf4j/index.html), and then use the Slf4j to Log4j 1.x bridge.

Alternatively you may do this by using the Log4j 1.x bridge as described in [Log4j 2.x migration docs](https://logging.apache.org/log4j/2.x/manual/migration.html#Log4j1.2Bridge).

---
