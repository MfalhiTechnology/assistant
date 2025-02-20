---

copyright:
  years: 2015, 2021
lastupdated: "2021-03-01"

subcollection: assistant

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Securing your data
{: #information-security}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions.
{: shortdesc}

**Notice:**
Clients are responsible for ensuring their own compliance with various laws and regulations, including the European Union General Data Protection Regulation (GDPR). Clients are solely responsible for obtaining advice of competent legal counsel as to the identification and interpretation of any relevant laws and regulations that may affect the clients’ business and any actions the clients may need to take to comply with such laws and regulations.

The products, services, and other capabilities described herein are not suitable for all client situations and may have restricted availability. IBM does not provide legal, accounting or auditing advice or represent or warrant that its services or products will ensure that clients are in compliance with any law or regulation.

If you need to request GDPR support for {{site.data.keyword.cloud}} {{site.data.keyword.watson}} resources that are created

- In the European Union, see [Requesting support for IBM Cloud Watson resources created in the European Union](/docs/watson/getting-started-gdpr-sar?topic=watson-gdpr-sar#request-EU){: external}.
- Outside the European Union, see [Requesting support for resources outside the European Union](/docs/watson/getting-started-gdpr-sar?topic=watson-gdpr-sar#request-non-EU){: external}.

## European Union General Data Protection Regulation (GDPR)
{: #information-security-gdpr}

IBM is committed to providing our clients and partners with innovative data privacy, security and governance solutions to assist them on their journey to GDPR compliance.

Learn more about IBM's own GDPR readiness journey and our GDPR capabilities and offerings to support your compliance journey [here](https://www.ibm.com/data-responsibility/gdpr/){: external}.

## Health Insurance Portability and Accountability Act (HIPAA)
{: #information-security-hipaa}

US Health Insurance Portability and Accountability Act (HIPAA) support is available for Enterprise plans that are hosted in the Washington, DC location created on or after 1 April 2019. For more information, see [Enabling EU and HIPAA supported settings](/docs/account?topic=account-eu-hipaa-supported#eu-hipaa-supported){: external}.

Do not add personal health information (PHI) to the training data (entities and intents, including user examples) that you create. In particular, be sure to remove any PHI from files that contain real user utterances that you upload to mine for intent or intent user example recommendations.

## Opting out of log data use
{: #information-security-log-opt-out}

IBM uses log data, Enterprise plan data excluded, to continually learn from and improve the {{site.data.keyword.conversationshort}} product. The logged data is not shared or made public.

To prevent IBM from using your log data for general service improvements, complete one of the following tasks: 

- If you are using a custom application, for each API `/message` request, set the `X-Watson-Learning-Opt-Out` header parameter to `true`.

  For more information, see [Data collection](https://cloud.ibm.com/apidocs/assistant/assistant-v2#data-collection){: external}.
- If you are using the web chat integration, add the `learningOptOut` parameter to the script that you embed in your web page, and set it to `true`. 

  For more information, see [Configuration](https://integrations.us-south.assistant.watson.cloud.ibm.com/web/developer-documentation/api-configuration){: external}.

## Labeling and deleting data in Watson Assistant
{: #information-security-gdpr-wa}

Do not add personal data to the training data (entities and intents, including user examples) that you create. In particular, be sure to remove any personally-identifiable information from files that contain real user utterances that you upload to mine for user example recommendations.

**Note:** Experimental and beta features are not intended for use with a production environment and therefore are not guaranteed to function as expected when labeling and deleting data. Experimental and beta features should not be used when implementing a solution that requires the labeling and deletion of data.

If you need to remove a customer's message data from a {{site.data.keyword.conversationshort}} instance, you can do so based on the customer ID of the client, as long as you associate the message with a customer ID when the message is sent to {{site.data.keyword.conversationshort}}.

- The preview and automatic Facebook integrations do not support the labeling and therefore deletion of data based on customer ID. These integration types should not be used in a solution that must support the ability to delete data based on a customer ID.
- For Intercom, the `customer_id` is the `user_id` prepended with `intercom_`. The Intercom `user_id` property is the `id` of the `author` message object in the Conversation Model that is defined by Intercom.
  
  - To get the ID, open the channel from a web browser. Open the web developer tools to view the console. Look for `author`.

  The full customer ID looks like this: `customer_id=intercom_5c499e5535ddf5c7fa2d72b3`.
- For Slack, the `customer_id` is the `user_id` prepended with `slack_`. The Slack `user_id` property is a concatenation of the team ID, such as `T09LVDR7Y`, and the member ID of the user, such has `W4F8K9JNF`. For example: `T09LVDR7YW4F8K9JNF`.

  - To get the team ID, open the channel from a web browser. Open the web developer tools to view the console. Look for `[BOOT] Initial team ID`.
  - You can copy the member ID from the user's Slack profile. 
  - To get the IDs programmatically, use the Slack API. For more information, see [Overview](https://api.slack.com/apis){: external}.
  The full customer ID looks like this: `customer_id=slack_T09LVDR7YW4F8K9JNF`.
- For the web chat integration, the service takes the `user_id` that is passed in and adds it as the `customer_id` parameter value to the `X-Watson-Metadata` header with each request.

### Before you begin
{: #information-security-delete-user-data-prereqs}

To be able to delete message data associated with a specific user, you must first associate all messages with a unique **customer ID** for each user. To specify the **customer ID** for any messages sent using the `/message` API, include the `X-Watson-Metadata: customer_id` property in your header. For example:

```sh
curl -X POST -u "apikey:3Df... ...Y7Pc9"
 --header
   'Content-Type: application/json'
   'X-Watson-Metadata: customer_id=abc'
 --data
   '{"input":{"text":"hello"}}'
  '{url}/v2/assistants/{assistant_id}/sessions/{session_id}/message?version=2019-02-28'
```
{: pre}

where {url} is the appropriate URL for your instance. For more details, see [Service endpoint](https://cloud.ibm.com/apidocs/assistant/assistant-v2#service-endpoint){: external}.

The `customer_id` string cannot include the semicolon (`;`) or equal sign (`=`) characters. You are responsible for ensuring that each `customer ID` property is unique across your customers.
{: note}

You can pass multiple **customer ID** values with semicolon-separated `customer_id={value}` pairs. For example: `'X-Watson-Metadata: customer_id=abc;customer_id=xyz'`

If you add a search skill to an assistant, user input that is submitted to the assistant is passed to the {{site.data.keyword.discoveryshort}} service as a search query. If the {{site.data.keyword.conversationshort}} integration provides a customer ID, then the resulting `/message` API request includes the customer ID in the header, and the ID is passed through to the {{site.data.keyword.discoveryshort}} `/query` API request. To delete any query data that is associated with a specific customer, you must send a separate delete request directly to the {{site.data.keyword.discoveryshort}} service instance that is linked your the assistant. See the {{site.data.keyword.discoveryshort}} [information security](/docs/discovery/information-security?topic=discovery-information-security) topic for details.

### Querying user data
{: #information-security-query-customer-id}

Use the v1 `/logs` method `filter` parameter to search an application log for specific user data. For example, to search for data specific to a `customer_id` that matches `my_best_customer`, the query might be:

``` sh
curl -X GET -u "apikey:3Df... ...Y7Pc9" \
"{url}/v2/assistants/{assistant_id}/logs?version=2020-04-01&filter=customer_id::my_best_customer"
```
{: pre}

where {url} is the appropriate URL for your instance. For more details, see [Service endpoint](/apidocs/assistant/assistant-v2#service-endpoint){: external}.

See the [Filter query reference](/docs/assistant?topic=assistant-filter-reference) for additional details.

### Deleting data
{: #information-security-delete-data}

To delete any message log data associated with a specific user that your assistant might have stored, use the `DELETE /user_data` v1 API method. Specify the customer ID of the user by passing a `customer_id` parameter with the request.

Only data that was added by using the `POST /message` API endpoint with an associated customer ID can be deleted using this delete method. Data that was added by other methods cannot be deleted based on customer ID. For example, entities and intents that were added from customer conversations, cannot be deleted in this way. Personal Data is not supported for those methods.

**IMPORTANT**: Specifying a `customer_id` will delete *all* messages with that `customer_id` that were received before the delete request, across your entire {{site.data.keyword.conversationshort}} instance, not just within one skill.

As an example, to delete any message data associated with a user that has the customer ID `abc` from your {{site.data.keyword.conversationshort}} instance, send the following cURL command:

```sh
curl -X DELETE -u "apikey:3Df... ...Y7Pc9" \
"{url}/v2/user_data?customer_id=abc&version=2020-04-01"
```
{: pre}

where {url} is the appropriate URL for your instance. For more details, see [Service endpoint](/apidocs/assistant/assistant-v2#service-endpoint){: external}.

An empty JSON object `{}` is returned.

For more information, see the [API reference](/apidocs/assistant/assistant-v2#deleteuserdata).

**Note:** Delete requests are processed in batches and may take up to 24 hours to complete.
