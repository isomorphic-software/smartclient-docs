# DataSource Facade pattern

[← Back to API Index](../reference.md)

---

## KB Topic: DataSource Facade pattern

### Description
The DataSource Facade pattern means implementing a DataSource that fulfills its [DSRequests](../reference.md#object-dsrequest) by passing them on to another DataSource.

This can be useful for:

*   various testing purposes, such as introducing long delays or intermittent failures to see how your code responds
*   implementing application-specific caching behaviors that go beyond [DataSource.cacheAllData](../classes/DataSource.md#attr-datasourcecachealldata) or automatic caching done by [ResultSet](../classes/ResultSet.md#class-resultset)
*   providing DSResponses that make use of data from two or more DataSources, by sending DSRequests to those other DataSources, waiting for both to respond, then combining the response data (note that for something like a SQL join, you should instead use [DataSourceField.includeFrom](../classes/DataSourceField.md#attr-datasourcefieldincludefrom) if you have SmartClient Pro or better)
*   slight modifications of data returned by another DataSource (although consider just using [OperationBinding.operationId](../classes/OperationBinding.md#attr-operationbindingoperationid) for this)

This facade pattern can be implemented either server-side or client-side:

*   server-side (SmartClient Pro or better), implement a custom DataSource (see QuickStart Guide) and implement the server-side API DataSource.execute() by calling DataSource.execute() on some other DataSource, then return the DSResponse that results.
*   client-side, use [dataProtocol:"clientCustom"](../classes/DataSource.md#attr-datasourcedataprotocol). The [FacadeDataSource](../classes/FacadeDataSource.md#class-facadedatasource) provides a specific implementation that is useful for testing purposes. Alternative, the code below shows the simplest possible code for the facade pattern when implemented client-side via `dataProtocol:"clientCustom"` - requests are forwarded to another DataSource, and the responses are returned completely unchanged.

```
 var facadeDataSource = isc.DataSource.create({
     dataProtocol: "clientCustom",
     inheritsFrom: "supplyItem",

     transformRequest : function (dsRequest) {
         var superDS = isc.DataSource.get(this.inheritsFrom),
             selfDS = this;

         var derivedDSRequest = selfDS.cloneDSRequest(dsRequest);
         derivedDSRequest.showPrompt = false;
         derivedDSRequest.callback = function (dsResponse, data, derivedDSRequest) {
             selfDS.processResponse(dsRequest.requestId, superDS.cloneDSResponse(dsResponse));
         };

         superDS.execute(derivedDSRequest);

         return dsRequest.data;
     }
 });
 
```

Check out [this example](https://www.smartclient.com/smartclient-latest/showcase/?id=loadedValues) of the DataSource facade pattern being used to create a DataSource that may work with already loaded data, or may use another DataSource to fulfill its requests.

---
