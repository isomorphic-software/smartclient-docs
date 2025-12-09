# Handling concurrent edits in SmartClient DataSources

[← Back to API Index](../reference.md)

---

## KB Topic: Handling concurrent edits in SmartClient DataSources

### Description
How do SmartClient DataSources handle multiple users making changes to the same record?

Consider a scenario where two users - _userA_ and _userB_ - are logged into the same application and viewing the same set of records in a SmartClient application:

*   _userA_ makes a change to a record and [saves the edit](../classes/DynamicForm.md#method-dynamicformsavedata)
*   _userB_ then makes another change to the same record and saves their edit

By default SmartClient dataSources have simple "most recent edit wins" behavior, so the changes made by userB will be preserved in the dataSource permanent storage - though if [DataSource.sparseUpdates](../classes/DataSource.md#attr-datasourcesparseupdates) is false, any changes made by _userA_ to fields that were not explicitly edited by _userB_ will also be preserved.

In this case when _userA_ performs their first edit (before _userB_ has attempted a save), _userB_ will not see _userA_'s changes unless they explicitly re-fetch the data. Similarly, _userA_ will not see _userB_'s subsequent edit without a re-fetch.

In many applications this behavior is acceptable but there may be cases where users will need to see other users' updates as they occur, and simple "last edit wins" is not sufficient. There are 2 things you can do to make this more sophisticated:

**Broadcasting changes:**  
The [DataSource.updateCaches](../classes/DataSource.md#method-datasourceupdatecaches) method is a way to notify a DataSource that a change has occurred. It will update its client-side caches to reflect the change and databound components showing the record will be refreshed as appropriate.

Developers using the SmartClient server and [messaging](messaging.md#kb-topic-real-time-messaging) may use this feature to propogate changes from the server to the client.

See this [blog post](https://isomorphic.atlassian.net/wiki/spaces/Main/pages/525130/How+to+propagate+data+source+changes+to+all+clients+by+using+the+Real-Time+Messaging+Module) for details on this approach.  
_Note: The sample project in this post is a SmartGWT project rather than SmartClient project. This means the client-side code to handle the server response is written in Java rather than JavaScript - but the methodology directly translates to SmartClient JavaScript and should be easy to understand._

**Detecting concurrent edits:**  
Note that even if an application is using Realtime Messaging or some similar approach to notify users of external edits as soon as they occur, it is still possible to get concurrent edit attempts on the same record.

In our original scenario - if _userB_ hit their save button after _userA_ but before the server had processed _userA_'s request, _userB_'s edit would essentially be based on "stale" values.

One way to detect this is to have custom server logic compare [DSRequest.oldValues](../classes/DSRequest.md#attr-dsrequestoldvalues) with the current values for the edited record and disallow the edit when this occurs.

See this [blog post](https://isomorphic.atlassian.net/wiki/spaces/Main/pages/525045/Detecting+concurrent+edits+with+long+transactions) for details on using oldValues to detect concurrent edits.  
_Once again, this post uses a SmartGWT Java project to demonstrate the approach._

---
