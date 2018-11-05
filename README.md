# personalChatBot
Answers questions regarding tribhuvans tech skills based on resume 

This bot has been created using [Microsoft Bot Framework][10], it shows how to create a simple echo bot with state. The bot maintains a simple counter that increases with each message from the user. This bot example uses [`restify`][1].

# How bot works?
1. The message activity carries conversation information between the parties
2. Activities arrive at the bot from the Bot Framework Service via an HTTP POST request
3. Processing starts with the HTTP POST request, with the activity information carried as a JSON payload, arriving at the web server from bot frame work, this will be in node.js.
4. Adapter is the conductor of the framework, it creates activity object and hands over to adapter process activity method along with authentication details.
5. After receiving object adapter creates turn context object and calls the middleware
6. Processing continues to the bot logic after middleware, the pipeline completes, and the adapter disposes of the turn context object
7. Application logic goes in bots turn handler,  turn handler is responsible for response for any given inbound activity. these reponse are again sent out using turn context send activity method, calling send activity will send msg to user channel
8. Middleware operate on the activity both before and after the bot's turn handler and have access to the turn context for that activity
9. the final stage of the middleware pipeline is a callback to invoke the turn handler of the bot, before returning up the stack
10. The turn context provides activity response methods to allow code to respond to an activity, they are send activity, update activity, delete activity
11. Response methods  runs in an asynchronous process
12. send activities method, which allows you to send an ordered set of activities, to make sure that they make sense in whatever order they are received by the user
13. Each new activity gets a new thread to execute on. When the thread to process the activity is created, the list of handlers for that activity is copied to that new thread. No handlers added after that point will be executed for that specific activity event






# To run the bot
- Install modules and start the bot
    ```bash
    npm i & npm start
    ```
    Alternatively you can also use nodemon via
    ```bash
    npm i & npm run watch
    ```

# Testing the bot using Bot Framework Emulator
[Microsoft Bot Framework Emulator][2] is a desktop application that allows bot developers to test and debug their bots on localhost or running remotely through a tunnel.

- Install the Bot Framework emulator from [here][3]

## Connect to bot using Bot Framework Emulator **V4**
- Launch Bot Framework Emulator
- File -> Open Bot Configuration
- Select `personalChatBot.bot` file

# Bot state
A key to good bot design is to track the context of a conversation, so that your bot remembers things like the answers to previous questions. Depending on what your bot is used for, you may even need to keep track of conversation state or store user related information for longer than the lifetime of one given conversation.

In this example, the bot's state is used to track number of messages.

 A bot's state is information it remembers in order to respond appropriately to incoming messages. The Bot Builder SDK provides classes for [storing and retrieving state data][4] as an object associated with a user or a conversation.

    - Conversation properties help your bot keep track of the current conversation the bot is having with the user. If your bot needs to complete a sequence of steps or switch between conversation topics, you can use conversation properties to manage steps in a sequence or track the current topic. Since conversation properties reflect the state of the current conversation, you typically clear them at the end of a session, when the bot receives an end of conversation activity.

    - User properties can be used for many purposes, such as determining where the user's prior conversation left off or simply greeting a returning user by name. If you store a user's preferences, you can use that information to customize the conversation the next time you chat. For example, you might alert the user to a news article about a topic that interests her, or alert a user when an appointment becomes available. You should clear them if the bot receives a delete user data activity.

# Deploy this bot to Azure
You can use the [MSBot][5] Bot Builder CLI tool to clone and configure the services this sample depends on.

To install all Bot Builder tools -

Ensure you have [Node.js](https://nodejs.org/) version 8.5 or higher

```bash
npm i -g msbot chatdown ludown qnamaker luis-apis botdispatch luisgen
```

To clone this bot, run
```
msbot clone services -f deploymentScripts/msbotClone -n myChatBot -l <Azure-location> --subscriptionId <Azure-subscription-id>
```

# Further reading
- [Azure Bot Service Introduction][6]
- [Bot State][7]
- [Write directly to storage][8]
- [Managing conversation and user state][9]


[1]: https://www.npmjs.com/package/restify
[2]: https://github.com/microsoft/botframework-emulator
[3]: https://aka.ms/botframework-emulator
[4]: https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-v4-state?view=azure-bot-service-4.0&tabs=js
[5]: https://github.com/microsoft/botbuilder-tools
[6]: https://docs.microsoft.com/en-us/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0
[7]: https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-storage-concept?view=azure-bot-service-4.0
[8]: https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-v4-storage?view=azure-bot-service-4.0&tabs=jsechoproperty%2Ccsetagoverwrite%2Ccsetag
[9]: https://docs.microsoft.com/en-us/azure/bot-service/bot-builder-howto-v4-state?view=azure-bot-service-4.0&tabs=js
[10] https://dev.botframework.com
