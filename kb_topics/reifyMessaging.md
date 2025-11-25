# Reify Messaging

[← Back to API Index](../main.md)

---

## KB Topic: Reify Messaging

### Description
Reify allows you to send two different kind of messages from your applications: Email and SMS.

**Email**

There is a special DataSource named 'isc\_sendEmail', which you can directly use from your app. The following fields are required to send this kind of message:

*   **to**: indicates the email accounts of the destinataries. Use commas (',') in order to use more than one destinatary.
*   **subject**: indicates the topic of the email.
*   **message**: indicates the message to send.

You need to set up the following entry in the server.properties file in order to use this feature:

*   **reify.emailFrom**: the email account used as 'from' in the email message.

Also, you can check the [Mail overview](../classes/Mail.md#class-mail) to know how to set up access to an SMTP server and complete the configuration to use this feature.

**SMS**

There is a special DataSource named 'isc\_sendSMS', which you can directly use from your app. The following fields are required to send this kind of message:

*   **to**: phone numbers of the destinataries that will receive the message. Use commas (',') in order to use more than one phone number.
*   **message**: message to send.

Also, Reify uses a specific Twilio library to achieve this. You need to set up the following entries in the server.properties file in order to use this feature:

*   **twilio.ACCOUNT\_SID**: identifier of the account, which acts as a username.
*   **twilio.AUTH\_TOKEN**: acts as a password.
*   **twilio.twilioPhoneNumber**: Twilio phone number you get when setting up your account in Twilio.

You need to register in the Twilio website and set up your account in order to get the required values.

---
