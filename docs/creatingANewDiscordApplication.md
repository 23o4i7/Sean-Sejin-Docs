---
layout: default
title: Register a New Bot on Discord
nav_order: 3
---

# Register a New Bot on Discord
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Creating a new Discord application
In this task, we are going to walk through how to create a new Discord application in order to work with the library and the Discord API in general.

1. Once you enable developer mode with your account, navigate to the [Application page.](https://discord.com/developers/applications)<br><br>![newApplication1](../graphics/newApplication1.png)

2. When you are on the Application page, you can see the button, _**New Application**_.<br><br>![newApplication2](../graphics/newApplication2.png)

3. Click the button, then you will see a pop up asking you to create the application name. Give the application a name and click _**Create**_.<br><br>![newApplication3](../graphics/newApplication3.png)

---

## Register the new application as a bot
This part will help you how to register the new application to create a bot.

1. After the application name is created, you will see the general information page. On the left side of the page, you will be able to see **Bot**.<br><br>![newApplication1](../graphics/registration1.png)

2. Go to the _**Bot**_ tab and click _**Add Bot**_. You should confirm by clicking _**Yes, do it!**_<br><br>![newApplication1](../graphics/registration2.png)

3. After this step, you will see the default settings for Public Bot(checked) and Require OAuth2 Code Grant(unchecked). However, make both _**unchecked**_ to keep your bot private.<br><br>![newApplication1](../graphics/registration3.png)

4. Congratulations! Your bot has been created. Now, click the _**Copy**_ to copy the token. 
<br><br>![newApplication1](../graphics/registration4.png)

> This token is your bot’s password, so _**be extra careful**_ not to share it with anyone. It will give others authorization to log in to your bot. If the token gets shared, click the _**Regenerate**_ to create a new token for your bot.