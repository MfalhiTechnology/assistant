---

copyright:
  years: 2015, 2021
lastupdated: "2021-03-16"

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

# Web chat release notes
{: #release-notes-chat}

Find out what's new in the web chat integration.
{: shortdesc}

The web chat change log lists changes ordered by version number. For more information about the web chat, see [Integrating the web chat with your website](/docs/assistant?topic=assistant-deploy-web-chat).

For information about new features and improvements to the core {{site.data.keyword.conversationshort}} product, see [Release notes](/docs/assistant?topic=assistant-release-notes).

## Controlling the version
{: #release-notes-chat-version}

If you want to evaluate changes that are introduced in a web chat release before you apply them to your deployment, you can set a version of your web chat. For more information, see [Versioning](/docs/assistant?topic=assistant-web-chat-basics/#web-chat-basics-versions).

## 4.0.0
{: #4.0.0}

*Release date: 16 March 2021*

- **Session history now generally available**: Session history allows your web chats to maintain conversation history and context when users refresh a page or change to a different page on the same website. It is enabled by default. For more information about this feature, see [Session history](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history){: external}.
    
  Session history persists within only one browser tab, not across multiple tabs. The dialog provides an option for links to open in a new tab or the same tab. See [this example](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history#Tutorial1) for more information on how to format links to open in the same tab.
  
  Session history saves changes that are made to messages with the [pre:receive event](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#prereceive) so that messages still look the same on rerender. This data is only saved for the length of the session. If you prefer to discard the data, set `event.updateHistory = false;` so the message is rerendered without the changes that were made in the pre:receive event.

  [instance.updateHistoryUserDefined()](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#updateHistoryUserDefined) provides a way to save state for any message response. With the state saved, a response can be rerendered with the same state. This saved state is available in the `history.user_defined` section of the message response on reload. The data is saved during the user session. When the session expires, the data is discarded.
  
  Two new history events, [history:begin](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#historybegin) and [history:end](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-events#historyend) announce the beginning and end of the history of a reloaded session. These events can be used to view the messages that are being reloaded. The history:begin event allows you to edit the messages before they are displayed.

  See this example for more information on saving the state of [customResponse](https://web-chat.global.assistant.watson.cloud.ibm.com/testfest.html?to=api-events#customresponse) types in session history.

- **Channel switching**: You can now create a dialog response type to functionally generate a connect-to-agent response within channels other than web chat. If a user is in a channel such as Slack or Facebook, they can trigger a channel transfer response type. The user receives a link that forwards them to your organization's website where a connection to an agent response can be started within web chat. <!--For more information, see [Adding a Channel transfer response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-channel-transfer).-->

## 3.5.0
{: #3.5.0}

*Release date: 17 February 2021*

- **Session history (beta)**: Web chat session history (beta) is now available. This feature makes it possible to maintain conversation history and context when customers refresh the page or navigate to a different page on the same website. For more information about this beta feature, see [Session history (beta)](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-session-history).

## 3.4.1
{: #3.4.1}

*Release date: 2 February 2021*

- Made an accessibility enhancement to the chat history. Now, you can use keys to navigate the messages by clicking the chat history, pressing Enter, and then using the arrow keys to move from one message to the next.
- The `instance.updateAssistantInputFieldVisibility()` method was added. You can use it to hide or show the text input field. For example, you might use the `pre:receive` event to check whether an options response type is being returned and if so, hide the text field so the user is forced to pick one of the available options only.
- The `instance.getState()` method was added. You can use it to check for specific conditions, such as `isWebChatOpen`, before you perform an action that might rely on the condition being true.

For more information about the new methods, see [Instance methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods){: external}.

## 3.3.2
{: #3.3.2}

*Release date: 17 December 2020*

- Addressed accessibility issues.

## 3.3.1
{: #3.3.1}

*Release date: 3 December 2020*

- The translated strings in the [language files](https://github.com/watson-developer-cloud/assistant-web-chat/tree/main/languages) were revised and improved.
- An error message is shown now if a Java Web Token (JWT) that is provided with an incoming message is invalid. If the first JWT fails when the web chat opens, an error message is displayed in place of the web chat window that says, `There was an error communicating with Watson Assistant`. If the initial JWT is valid, but the token for a subsequent message is invalid, a more discreet error message is displayed in response to the insecure input.
- Bug fixes.

## 3.3.0
{: #3.3.0}

*Release date: 23 November 2020*

- Added support for passing contextual information to a service desk agent from web chat.
- You can now customize a `user_defined` response type. For more information, see the [Custom response type tutorial](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=tutorials-user-defined-response).
- Bug fixes.

## 3.2.1
{: #3.2.1}

*Release date: 2 November 2020*

- **Bug fix**: Fixing a bug that prevented the web chat integration preview from working after security was enabled.

## 3.2.0
{: #3.2.0}

*Release date: 26 October 2020*

- **Security improvement**: If you enable security, you no longer need to include the `identityToken` property when the web chat is loaded on a web page. If a token is not initially provided, the existing identityTokenExpired event will be fired when the web chat is first opened to obtain one from your handler.

- **Starter kit update**: The starter kit now allow you to customize the timeout that occurs when the web chat integration checks whether any service desk agents are online.

## 3.1.1
{: #3.1.1}

*Release date: 22 October 2020*

- **Accessibility improvement**: Changed how the announcement text is generated to prevent announcements from being duplicated. Announcement text is hidden text that is provided for use by screen readers to indicate when dynamic web page changes occur.

## 3.1.0
{: #3.1.0}

*Release date: 8 October 2020*

- **Suggestions now allow for trial and error**: If customers select a suggestion and find that the response is not helpful, they can open the suggestions list again and try a different suggestion.

## 3.0.0
{: #3.0.0}

*Release date: 22 September 2020*

- **Choose when a link to support is included in suggestions**: The Suggestions beta feature has moved to its own tab. Now you can enable suggestions even if your web chat is not set up to connect to a service desk solution. That's because now you can control if and when the option to connect to customer support is available from the suggestions list. For more information, see [Showing more suggestions](/docs/assistant?topic=assistant-deploy-web-chat#deploy-web-chat-alternate).

- **Search result format change**: To support the ability to show more than 3 search results in a response, the search skill response type format changed. If you are using `pre:receive` or `receive` handlers to process search results, you might need to update your code. The `results` property was replaced by the `primary_results` and `additional_results` properties. For more information about the new search skill response type format, see the [API reference](https://cloud.ibm.com/apidocs/assistant/assistant-v2#message){: external}.

- **Language pack key change**: Due to improvements that were made to allow you to specify separate chat transfer messages for situations where agents are available and unavailable, the [language source file](https://github.com/watson-developer-cloud/assistant-web-chat/tree/master/languages) was updated. The `agent_chatDescription` was renamed to `default_agent_availableMessage` and another key (`default_agent_unavailableMessage`) was added. If you defined a custom string for the `agent_chatDescription` key, you must modify your code to reflect this change. For more information about the new availability messages and how they are used, see [Adding a *Connect to human agent* response type](/docs/assistant?topic=assistant-dialog-overview#dialog-overview-add-connect-to-human-agent).

## 2.4.0
{: #2.4.0}

*Release date: 2 September 2020*

- **Add a home screen**: Ease your customers into the conversation by adding a home screen to your web chat window. The home screen greets your customers and shows conversation starter messages that customers can click to submit to the assistant. For more information about this beta feature, see [Adding a home screen](/docs/assistant?topic=assistant-deploy-web-chat#deploy-web-chat-home-screen).

## 2.3.0
{: #2.3.0}

*Release date: 10 August 2020*

- **Introducing *Suggestions***: Enable this beta feature to show a helper icon in the chat that customers can click to see alternate topics or to connect to an agent. For more information, see [Showing more suggestions](/docs/assistant?topic=assistant-deploy-web-chat#deploy-web-chat-alternate).

- **Search results are now expandable**: When search results are displayed in the web chat, users can click **Show more** to see more of the search result text.

## 2.2.0
{: #2.2.0}

*Release date: 29 July 2020*

- **Introduced the `instance.writeableElements()` method**: The `instance.writeableElements()` method gives you zones in the web chat user interface where you can embed your own content. For example, you can add content to the end of the header where it is displayed even as the chat content changes. Or you can add custom content that is displayed before the welcome node. For more information, see [Instance methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#writeableelements){: external}.

- **Gave the *Send* button a new look** 

  Changed the icon from ![Arrow send icon](images/web-chat-send-old.png) to ![Paper airplane send icon](images/web-chat-send.png).

- **Securing your web chat is easier**: You no longer need to specify the `acr` claim when you define the JWT. The Authentication Context Class reference is managed by the web chat automatically.

- Improved the quality of non-English translations.

- Made a few minor bug fixes.

## 2.1.2
{: #2.1.2}

*Release date: 2 July 2020*

- **Fixed a loading issue**: Addressed an issue that prevented the web chat from loading properly for some deployments with short JWT expiration claims.

## 2.1.1
{: #2.1.1}

*Release date: 1 July 2020*

- **Service desk agent initials are displayed**: When the web chat transfers a user to a service desk agent, the agent's avatar is displayed in the chat window to identify messages sent from the service desk agent. If the agent does not have an avatar, the first initial of the agent's given name is displayed instead.

## 2.0
{: #2.0}

*Release date: 16 June 2020*

- **Versioning was added to web chat**: For more information, see [Versioning](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=key-concepts#versioning){: external}.

- **Added bidirectional support**: You can now use the `direction` parameter to choose whether to show text and elements in the web chat in right-to-left or left-to-right order. For more information, see  [Configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration){: external}.

- **Introduced the `instance.destroySession()` method**: The `instance.destroySession()` method removes all cookie and browser storage that is related to the current web chat session. You can use this method as part of your website logout sequence. For more information, see [Instance methods](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#destroySession){: external}.

## 1.5.3
{: #1.5.3}

*Release date: 14 April 2020*

- **The *Font family* field was removed from the configuration page**: The text that is displayed in the chat window uses the fonts: `IBMPlexSans, Arial, Helvetica, sans-serif`. If you want to use a different set of fonts, you can customize the CSS for your web chat implementation. For more information, see [Theming](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-instance-methods#theming).
- When your implementation does not specify a unique user ID, the web chat adds a first party cookie with a generated anonymous ID to use to identify the unique user. The generated cookie now expires after 45 days. For more information, see [GDPR and cookie policies](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=key-concepts#datapolicy){: external}.

## 1.5.2 
{: #1.5.2}

*Release date: 2 April 2020*

- **Introduced the `learningOptOut` parameter**: You can add the `learningOptOut` parameter and set it to `true` to add the `X-Watson-Learning-Opt-Out` header to each `/message` request that originates from the Web Chat. For more information about the header, see [Data collection](https://cloud.ibm.com/apidocs/assistant/assistant-v2#data-collection){: external}. For more information about the parameter, see [Configuration](https://web-chat.global.assistant.watson.cloud.ibm.com/docs.html?to=api-configuration){: external}.

## 1.4.0
{: #1.4.0}

*Release date: 20 March 2020*

- **Customize the CSS theme**: For more information, see [Theming](https://integrations.us-south.assistant.watson.cloud.ibm.com/web/developer-documentation/api-instance-methods#theming){: new_window}.
  
- **Shadow DOM is no longer used**: When you use custom response types or HTML in your dialog, you can apply CSS styles that are defined in your web page to the assistant's response. To override any default styling in the web chat, you must specify the `!important` modifier in your CSS. For more information, see [Rendering response types](https://integrations.us-south.assistant.watson.cloud.ibm.com/web/developer-documentation/api-render#html){: new_window}.
