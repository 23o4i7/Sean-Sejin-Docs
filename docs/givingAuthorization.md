---
layout: default
title: Authorize and Connect the Bot to Your Server
nav_order: 4
---

# Connecting the Bot To Your Server
{: .no_toc }

---

## Authorizing Bot Permissions

In this section, we will give the bot its necessary permissions, then we will create an invite link to add the bot to our server.

1. In the ***Bot** tab, go to _**OAuth2**_ and click _**URL Generator**_.<br><br>![newApplication1](../graphics/createapplication2.png)<br>

2. In the ***scopes*** table, click  ***bot*** and ***applications.commands*** under the _**Scopes**_ section.<br><br>![newApplication1](../graphics/authBot.png)<br>

3. Under the ***Bot Permissions*** table, choose the ***Admininstrator*** setting. Keep in mind you can restrict and remove permissions later.<br><br>![newApplication1](../graphics/authBot2.png)<br>

4. After choosing the necessary permissions for the bot, click the _**copy**_ to get a generated URL that can be used to invite the bot to a server.<br><br>![newApplication1](../graphics/authorization4.png)<br>

5. Paste the URL address into your browser, select your server, and click _**Authorize**_.<br><br>![newApplication1](../graphics/authorization5.png)<br>

6. You should be able to see the bot in your server on the users list.<br><br>![newApplication1](../graphics/authorization6.png)

---

## Conclusion
{: .no_toc }

Congratulations! Now that we've added the bot to our server, we can start writing the code for the bot.