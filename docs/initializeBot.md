---
layout: default
title: Initalize the Bot
nav_order: 5
---

# Initializing and Setting Up the Bot
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---


| ![warning](../graphics/warning2.png) |
|---|
| Before continuing, ensure that you have an IDE like Visual Studio Code, and Node.js installed on your machine. Next, check your Node.js version by opening any terminal, such as Command Prompt on Windows, or Terminal on a Mac or Linux machine. Inside the terminal, type `node -v`, and that will show you the Node.js version installed on your machine. Make sure that the version is greater than _`V16.6.0`_. |

Now that we've added the bot to our server, we can start building the brains and some basic functions for it.

## Creating the Initial Files

First, create a new folder to contain all of your files. Inside your folder, create three new files:

* `app.js`
* `token.json`

Now, open a terminal and move into the folder with the files you created using the command, `cd <folder path>`. To get the full path of a folder, follow this [tutorial for Windows](https://techdows.com/2022/01/windows-11-copy-as-path-and-its-shortcut.html), or this [tutorial for Mac](https://www.igeeksblog.com/how-to-copy-file-folder-path-from-mac-finder/#:~:text=Triple%2Dclick%20the%20file%20path,V%20wherever%20it%20is%20required.). 

Once you have moved into the folder, ***do not*** close this terminal, unless you are confident you can easily set it up again. You will need this instance of the terminal for more steps later on.

In the terminal, enter `npm init`. This will initialize the folder and allow you to easily keep track of files and different libraries you will need to use for this project. You will be prompted by the terminal and shown something like this.

![npminit](../graphics/npminit.png)

Hit **Enter** until you see the prompt for _`test command`_, or 4 times. For this field, write `nodemon app.js`. The `nodemon` command is for a library we will install later, which automatically re-runs Node.js apps when you make any changes. It is an incredibly important tool for any web-based application.

Once it completes, you should see two new files inside your folder:

* `package.json`
* `package-lock.json`

These files will store data and keep track of the different libraries that you may use in your project. Inside the ***package.json*** folder, you can also enter custom scripts that you can use for any purpose, for example, testing. 

Next, open the `token.json` folder. You will need to get your special token you received when you [created a new bot](https://23o4i7.github.io/Sean-Sejin-Docs/docs/creatingANewDiscordApplication/). Once you've got it, inside the file, write:

```json
{
    "token": "<your token here>"
}
```

This will keep your token more secure, as it is not directly accessible to anyone who can see your bot.

| ![warning](../graphics/important2.png) |
|---|
|<table> |
|  |
|If you plan on uploading this project to Git, create a `.gitignore` file with the following content:|
|``` |
|node_modules|
|token.json|
|``` |
|This will stop sensitive information from being published onto your Git repository.|
|  |
| </table> |

---

## Installing Libraries

By itself, JavaScript does not have the capability to create a bot that is integrated with Discord. This requires the use of libraries and modules that we will have to install on top  of our project.

First, go back to the terminal, and type in `npm install nodemon discord.js`. This will install two libraries, `nodemon`, which we will use to run the bot, and `discord.js`. Discord.js is a library built off of Discord's Application Programming Interface, or API. It allows you to get and send data directly via Discord. This is an incredibly powerful feature, and makes your job os creating a bot much easier. 

Open the `app.js` file, and at the top, write:

```js
// Require the neccessary libraries
const discord = require("discord.js");
const { token } = require('./token.json');


// Create client instance for your bot to log in
const client = new discord.Client({ intents: [discord.Intents.FLAGS.GUILDS] });

// When you bot has logged in, it will print out in the console "Ready!"
client.once('ready', () => {
    console.log('Ready!');
});

// Your bot will use this token to log in
client.login(token);
```

This code will log your bot into Discord and allow it to start running. Next, let's add some basic functionality for the bot to perform.

## Adding Basic Commands and Functions

Because this guide is only for a very simple and small-scale bot, we are able to put all the commands inside the `app.js` file. But as bots grow over time, the feasability of this will greatly decrease. As we add more and more functionality, we will fall victim to a trap known as "if-else hell".

To avoid this, we will use modular architecture to store different commands in different files. Our directory will look something like this:

```

discord_bot/
  |-- node_modules/
  |-- token.json
  |-- app.js
  |-- package.json
  |-- package-lock.json
  |-- runCommands.js
  |-- commands/
        |-- command1.js
        |-- command2.js

```

Now that we have an idea of what a bot should look like, let's start by making the `runCommands.js` file.

### runCommands.js