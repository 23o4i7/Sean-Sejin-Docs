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
| Before continuing, ensure that you have an IDE like Visual Studio Code, and Node.js installed on your machine. Next, check your Node.js version by opening any terminal, such as Command Prompt on Windows, or Terminal on a Mac or Linux machine. Inside the terminal, type `node -v`, and that will show you the Node.js version installed on your machine. Make sure that the version is greater than _`V16.9.0`_. |

Now that we've added the bot to our server, we can start building the brains and some basic functions for it.

## Creating the Initial Files

1. Create a new project folder to contain all of your files. Inside your folder, create two new files:
   * `app.js`
   * `token.json`<br><br>

2. Open a terminal ([Terminal in Windows](https://www.wikihow.com/Open-Terminal-in-Windows) or [Terminal in MacOS](https://support.apple.com/en-ca/guide/terminal/apd5265185d-f365-44cb-8b09-71a064a42125/mac)) and type `cd <folder path>` to move into your project folder ([How to get folder path in Windows](https://techdows.com/2022/01/windows-11-copy-as-path-and-its-shortcut.html) or [How to get folder path in MacOS](https://www.igeeksblog.com/how-to-copy-file-folder-path-from-mac-finder/#:~:text=Triple%2Dclick%20the%20file%20path,V%20wherever%20it%20is%20required.)). ***Do not*** close this terminal, unless you are confident you can easily set it up again. You will need this instance of the terminal to complete building your bot.<br><br>

3. Enter `npm init` in the terminal. This allows you to easily keep track of files and different libraries you will need to use for this project. You will then be prompted by this menu:<br><br>![npminit](../graphics/npminit.png)<br><br>

4. Hit **Enter** until you see the prompt for _`test command`_, or 4 times. For this field, write `nodemon app.js`. It will setup `nodemon`, a useful tool for any web application.

You will see two new files inside your folder:

* `package.json`
* `package-lock.json`

These store data and keep track of the different libraries that you may use in your project. Inside the ***package.json*** folder, you can also enter custom scripts that you can use for any purpose, for example, testing.

| ![important](../graphics/important2.png) |
|---|
|If you plan on uploading this project to Git, create a `.gitignore` file with `node_modules` and `token.json` inside. This will stop sensitive information from being published onto your Git repository. |

---

## Installing Libraries

By itself, JavaScript does not have the capability to create a bot that is integrated with Discord. This requires the use of libraries and modules that we will have to install on top  of our project.

1. Type in `npm install nodemon discord.js discord-api-types`. This will install three libraries, `nodemon`, `discord.js` and `discord-api-types`.<br><br>
   * `nodemon` is a library that watches your web app's directory for any changes or modifications. It will automatically restart or stop your app in the event of a modification or an error.
   * `discord.js` is a library built off of Discord's API. This allows you to get and send data directly via Discord, which is an incredibly powerful feature, and makes your job os creating a bot much easier.
   * `discord-api-types` is an extension of `discord.js` that allows you to create custom scripts and commands for Discord applications. We will use this library later to write some basic commands for the bot.<br><br>

2. In the `app.js` file, and at the top, write:<br><br>
    ```js
    // Creates a new session in Discord for your bot to log in and use to function

    // Require the neccessary libraries
    const fs = require('fs');
    const discord = require("discord.js");
    const { token } = require('./token.json');


    // Create client instance for your bot to log in
    const client = new discord.Client({ intents: [discord.Intents.FLAGS.GUILDS] });

    // Brings in commands from your /commands folder
    client.commands = new discord.Collection();
    const commandFiles = fs.readdirSync('./commands').filter(file => file.endsWith('.js'));

    // Imports commands
    for (const file of commandFiles) {
        const command = require(`./commands/${file}`);
        client.commands.set(command.data.name, command);
    }

    // Runs your commands
    client.on('interactionCreate', async interaction => {
        if (!interaction.isCommand()) return;

        const command = client.commands.get(interaction.commandName);

        if (!command) return;

        try {
            await command.execute(interaction);
        } catch (error) {
            console.error(error);
            await interaction.reply({ content: 'There was an error while executing this command!', ephemeral: true });
        }
    })

    // When the bot has logged in, it will print out in the console "Bot is online!"
    client.once('ready', () => {
        console.log('Bot is online!');
    })

    // Your bot will use its token to log in and connect to your server
    client.login(token);
    ```

<br>This code will log your bot into Discord and allow it to start running. Now, we can add some basic functionality for the bot.

---

## Adding Basic Commands and Functions

Because this guide is only for a very simple and small-scale bot, we are able to put all the commands inside the `app.js` file. But as bots grow over time, the feasability of this will greatly decrease. As we add more and more functionality, we will fall victim to a trap known as ["if-else hell"](https://www.freecodecamp.org/news/so-youre-in-if-else-hell-here-s-how-to-get-out-of-it-fc6407fec0e/).

To avoid this, we will use [modular architecture](https://codesource.io/how-to-modularize-javascript-code/) to store different commands in different files. Our project directory should end up looking something similar to this:

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

Now that we have an idea of what our bot should look like, let's start by making the `runCommands.js` file.

### runCommands.js

1. Enter `npm install @discordjs/rest discord-api-types` in your console. This is an extension for the `discord.js` library that you can use to write applications and functions using [REST API](https://www.redhat.com/en/topics/api/what-is-a-rest-api).<br><br>

2. Create a JavaScript file inside your project folder named `runCommands.js`. In this file, add:<br><br>
    ```js
    // Imports commands from command subfolder for app.js to use

    // Require files and modules
    const fs = require('fs');
    const { REST } = require('@discordjs/rest');
    const { Routes } = require('discord-api-types/v10');
    const { clientID, guildID, token } = require('./token.json');

    // Creates the list of commands from the /commands folder
    const commands = [];
    const commandFiles = fs.readdirSync('./commands').filter(file => file.endsWith('.js'));

    // Requires the commands into the app.js file
    for (const file of commandFiles) {
        const command = require(`./commands/${file}`);
        commands.push(command.data.toJSON());
    }

    // Creates REST API token
    const rest = new REST({ version: '10' }).setToken(token);

    // Verifies all commands are successfully read or will return an error 
    rest.put(Routes.applicationGuildCommands(clientID, guildID), { body: commands })
        .then(() => console.log('Successfully registered application commands.'))
        .catch(console.error);
    ``` 

3. Get your client ID by going back to your application in the developer portal, then clicking ***Copy*** under the Application ID. Save this client ID with your bot's token.<br><br>![clientID](https://github.com/23o4i7/Sean-Sejin-Docs/blob/gh-pages/graphics/clientID.png?raw=true)<br><br>
   
4. Get your guild ID by going back to your server and right clicking the server's name or icon. Select ***Copy ID***, and save this with your bot's token and client ID.<br><br>![guildID](../graphics/guildid.png)<br><br>

5. Put your [bot's token](https://23o4i7.github.io/Sean-Sejin-Docs/docs/creatingANewDiscordApplication/), client ID, and guild ID inside the `token.json` folder. <br><br>

    ```json
    {
        "token": "<Your token here>",
        "guildID": "<Your guild ID here>",
        "clientID": "<Your client ID here>"
    }
    ```

<br>

| ![important](../graphics/important2.png) |
|---|
| Same with your bot's token, your client and guild IDs are sensitive and ***should never be shared under any circumstance***. You can regenerate your client ID if needed, but not your guild ID.<br><br>You must store your guild and client IDs as ***strings*** not ***numbers***. You will not be able to run your application if you do so. |



Now that we've set up the bot to register commands, we can make the `/command` folder and start adding functions.

---

### Commands

First, create a new folder named, `commands` in your project folder. This folder will store all of the JavaScript files containing all of your different functions.

Now let's add two different commands to our bot. The first command will be a simple reply that we can trigger by greeting the bot, and the second will generate a random number between 1 and 100.

| ![warning](../graphics/important2.png) |
|---|
| When you create a slash command using the `SlashCommandBuilder` library, you will have to set a name for the command using the `.setName()` method. All command names must be all lowercase letters, they cannot contain numbers or uppercase letters, or else they will not work. |

#### hello.js

Create a new file inside your `/commands` folder named `hello.js`. Inside this file, write:

```js
const { SlashCommandBuilder } = require('@discordjs/builders');

module.exports = {
    data: new SlashCommandBuilder()
        .setName('hi')
        .setDescription('Greets the user back'),
    async execute(interaction) {
        return interaction.reply(`Hi ${interaction.user.username}!`);
    },
};
```

This command will activate whenever you type `/hi` in your server, and the bot will reply back to you with _`Hi <Your username>`_.
<br>

#### randomNumber.js

Create another file inside your `/commands` folder named `randomNumber.js`. Inside this file, write:

```js
const { SlashCommandBuilder } = require('@discordjs/builders');
const getRandomNumber = (range) => Math.floor(Math.random() * range);

module.exports = {
	data: new SlashCommandBuilder()
		.setName('randomnumber')
		.setDescription('Generates a number between 0 and 100'),
	async execute(interaction) {
		return interaction.reply(`Your number is ${getRandomNumber(100)}!`);
	},
};
```

This command will activate whenever you type `/randomnumber` in your server, and the bot will reply back with `Your number is <number>!`

---

## Conclusion
{: .no_toc }

Congratulations! You've now added some functions to your bot! If you want to add more commands, just follow the same steps above, and change the `.setName`, `.setDescription`, and `.reply` fields to whatever parameters you want!