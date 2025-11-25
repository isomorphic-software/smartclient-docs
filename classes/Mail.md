# Mail Documentation

[← Back to API Index](../main.md)

---

## Class: Mail

### Description
A `Mail` object describes an email that will be sent automatically by the SmartClient Server as part of a normal [DataSource](DataSource.md#class-datasource) operation. Mail definitions are part of an [OperationBinding](OperationBinding.md#class-operationbinding), and they can only be specified in a DataSource's XML definition. Despite the declarative nature of mail definitions, templating support via Velocity makes it very flexible; it is very easy to include values from records just fetched from permanent storage by this operation, for example. See [velocitySupport](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables) for an overview of SmartClient Server's pervasive support for templated declarative operations using Velocity.

The default context for the message is the dsResponse.data; that is, $foo in the message refers to the field "foo" in the DataSource response (the equivalent of calling dsResponse.getFieldValue("foo") in Java). You also have access to the normal Velocity variables described in the overview linked to above.

If multiple records appear in the dsResponse, one message will be sent per record in the response unless "multiple" is set to false. This allows a set of recipients to be selected by a "fetch" operationBinding and messages sent to each. This also means that if no data is selected by a fetch or affected by an update, no mail is sent.

If you have the [Transaction Chaining](../kb_topics/transactionChaining.md#kb-topic-transaction-chaining) feature (available in Power and better versions), all of the variables normally accessible in other Velocity contexts are available in the message template as well, for example: `$responseData.last('order').orderId`

You can provide the body of the email directly in the [messageTemplate](#attr-mailmessagetemplate) tag, or you can provide a filename in the [templateFile](#attr-mailtemplatefile) attribute, which tells SmartClient to use the contents of that file as the body of the email. If you provide neither of these, your email will have no body; if you provide both, SmartClient will ignore the file and just use the content directly provided.

**Mail server configuration in server.properties**  

Static mail server to use for sending emails can be configured in the [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) file. The following values can be provided:

`mail.system.mail.smtp.host`: The name of the SMTP server to use; defaults to "localhost"  
`mail.system.mail.smtp.port`: What port is the MTA listening on; defaults to 25  
`mail.system.mail.smtp.auth`: Whether this server requires authentication; defaults to false  
`mail.system.mail.smtp.user`: SMTP user, if authentication is on; no default  
`mail.system.mail.smtp.password`: Password, if authentication is on; no default  

Note that we will also pass any other properties that start `mail.system` through to the underlying Javamail `Session` object, so you can use Javamail features that aren't explicitly exposed by SmartClient's mail support. For example, many cloud-based SMTP providers require that you issue a STARTTLS command before authenticating; you can achieve this by adding the following line to [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file):

`mail.system.mail.smtp.starttls.enable: true`

**Mail server configuration in OperationBinding**  

Dynamic mail server can be configured in [DataSource.operationBindings](DataSource.md#attr-datasourceoperationbindings) under [`<mail>`](OperationBinding.md#attr-operationbindingmail) tag. This allows to alter mail server settings for different operations and depending on data using [Velocity templates](../kb_topics/velocitySupport.md#kb-topic-velocity-context-variables). Same values can be provided as in `server.properties` omitting "mail.system.mail.smtp" prefix, i.e. "host", "port", "auth", "user" and "password".

Just like in `server.properties` any other properties can be provided and will be passed through to the underlying Javamail `Session` object. Note that property names must omit "mail.smtp" prefix, for example:

`<starttls.enable>true</starttls.enable>`

### Groups

- mail

---
## Attr: Mail.messageTemplate

### Description
The text that will form the body of the mail message. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

You must specify either this property or [templateFile](#attr-mailtemplatefile), but clearly it makes no sense to specify them both.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.subject

### Description
The string to appear in the subject line of the message. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

If you specify a "Subject:" line in the body of your email, the subject will be parsed and this property will be ignored.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.to

### Description
Comma-separated list of recipients. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

If you specify a "To:" line in the body of your email, recipient addresses will be parsed and this property will be ignored.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.auth

### Description
Defines whether authentication is required by SMTP server that will send the email. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.messageData

### Description
Allows you to specify an alternative source of substitution values for the templating process (by default, the data record(s) returned by the DataSource operation are used). If set, this [VelocityExpression](../main_2.md#type-velocityexpression) should evaluate to a Java `Map` object, or a Java `List` containing only `Map`s.

For example, assuming you had suitable context stored in a `Map` that is held in the current session as attribute "foo", the following would cause the mail templating system to look in there for values when running substitution:

```
     messageData="$session.foo"
 
```

### Groups

- mail

**Flags**: IRA

---
## Attr: Mail.encoding

### Description
Used to override the character encoding we apply to the email body. If you do not set this property, it is derived from the [server.properties](../kb_topics/server_properties.md#kb-topic-serverproperties-file) setting `mail.system.default.encoding`, which is set to "UTF-8" by default. This setting should be appropriate for most use cases.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.port

### Description
Port of the SMTP server that will send the email. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.from

### Description
The email address the message will appear to come from. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

If you specify a "From:" line in the body of your email, the from address will be parsed and this property will be ignored.

Ordinarily, this property (or the parsed equivalent in the email body) is mandatory for all emails. However, if you specify the property `mail.system.mail.smtp.from` in `server.properties`, it will become the default "from" address, and this property becomes optional.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.templateFile

### Description
Qualified name of the file containing the message template, relative to webroot. Like all the other `VelocityExpression` properties of `Mail`, you can use Velocity substitution variables in this property. The content itself (ie, the contents of the file named in this property) can also contain Velocity substitutions, of course.

You must specify either this property or [messageTemplate](#attr-mailmessagetemplate), but clearly it makes no sense to specify them both.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.contentType

### Description
Used to override the content-type header applied to the email. Primarily used to send HTML emails rather than plain text ones (use "text/html" to do this).

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.host

### Description
Host of the SMTP server that will send the email. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.user

### Description
User if authentication is required by SMTP server that will send the email. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.replyTo

### Description
An email address to indicate as the reply-to address on the message. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.bcc

### Description
Comma-separated list of "BCC" recipients. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

If you specify a "Bcc:" line in the body of your email, recipient addresses will be parsed and this property will be ignored.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.password

### Description
Password if authentication is required by SMTP server that will send the email. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.cc

### Description
Comma-separated list of "CC" recipients. Like all other `String` properties of `Mail`, you can use Velocity substitution variables in this property.

If you specify a "Cc:" line in the body of your email, recipient addresses will be parsed and this property will be ignored.

### Groups

- mail

**Flags**: IR

---
## Attr: Mail.multiple

### Description
By default, multiple mail messages are sent if the dsResponse contains multiple records. Set this property to false to prevent this behavior.

### Groups

- mail

**Flags**: IR

---
