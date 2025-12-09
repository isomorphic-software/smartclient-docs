# Application Declaration Files

[← Back to API Index](../reference.md)

---

## KB Topic: Application Declaration Files

### Description
When using the SmartClient server, server side methods written in java can be directly invoked from client side code via the [DMI.call](../classes/DMI.md#classmethod-dmicall) API.

In order to support this an application configuration file needs to be present on your server. This file lists out what server side methods are exposed for direct invocation. The application configuration file should be named `_appID_.app.xml` (where _"appID"_ is some arbitrary id for your application) and must be present at the location specified by the `project.apps` setting in the [server.properties](server_properties.md#kb-topic-serverproperties-file) file.

The application declaration should be written in xml, and should contain a `rpcBindings` block, which holds [ServerObject](../reference_2.md#object-serverobject) definitions for each exposed method. Here's an example demonstrating the specified format:

```
    <Application>
        <rpcBindings>
            <ServerObject ID="MathUtil" className="com.example.package.MathUtil">
                <visibleMethods>
                    <method name="addIntegers"/>
                </visibleMethods>
            </ServerObject>
        </rpcBindings>
    </Application>
 
```
In this example we're exposing a method _"addIntegers"_ on the server side java class `com.example.package.MathUtil`. A developer could then call DMI.call(...) on the client side code to invoke this method on the server, and get at the returned value in the [RPCResponse](../classes/RPCResponse.md#class-rpcresponse) passed to the [RPCCallback](../classes/Callbacks.md#method-callbacksrpccallback). Note that the application config file does not explicitly list out a method signature - the appropriate method to call is detected automatically based on the parameters passed to DMI.call on the client side.

The method may be also written using [Server Scripting](serverScript.md#kb-topic-server-scripting) if it is short or if it is needed to add fuctionality to the referred `ServerObject` without modyfing its Java code. The example above may be extended with the `addAbsIntegers` method imlpemented using groovy script, which from the client perspective can be called the same way as the `addIntegers` method above:

```
    <Application>
        <rpcBindings>
            <ServerObject ID="MathUtil" className="com.example.package.MathUtil">
                <visibleMethods>
                    <method name="addIntegers"/>
                    <method name="addAbsIntegers" language="groovy" args="values">
                        <script>
                            int res = 0;
                            for (int i: values) {
                                res += Math.abs(i);
                            }
                            return res;
                        </script>
                    </method>
                </visibleMethods>
            </ServerObject>
        </rpcBindings>
    </Application>
 
```
See the [DMI overview](dmiOverview.md#kb-topic-direct-method-invocation) for further information on Direct Method Invocation in SmartClient.

---
