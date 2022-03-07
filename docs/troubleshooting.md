---
layout: default
title: Troubleshooting
nav_order: 100
---

# Troubleshooting
{: .no_toc }

| Symptoms | Probable Causes | Action |
|----|----|----|
| `S[50001]: Missing Access` | Your guild ID or client ID are incorrect, or you have not connected your bot to your server before running it. | Double check your guild and client IDs in your `token.json` file that they are correct and are strings. Also, check if your bot has been added to your server. |
| `SyntaxError: Invalid regular expression flags` | Your Node.js version is older than 16.9.0 | Double check your node version by typing `node -v` in your console, or download the newest version [here](https://nodejs.org/en/). |
| `SyntaxError: Unexpected token` | Your Discord Bot's token is incorrect, or you regenerated a new one | Double check your `token.json` file to make sure you token is correct and does not include any trailing spaces. Also check if you regenerated your token, and re-copy it in. |
| Error contains `ZodError` | A name, description, or reply has been set incorrectly in one of your command files. | Double check the names of all your commands in the `.setName()` field to make sure you only have lowercase letters as your command name. Also check you have not left out the description or reply fields in your file. |
| Error contains `Invalid Form Body` | You have given your both an invalid command, the bot is trying to do something you haven't allowed it to do, or the bot does not know what you are trying to do. | First, re-register your commands by typing `node runCommands.js` in your terminal. Then, restart the bot either by typing `rs` into the terminal if you are using nodemon, or use **Ctrl+C**. Otherwise, you will have to look through [Discord's error code table](https://discord.com/developers/docs/topics/opcodes-and-status-codes#json-json-error-codes) to see which error you got. |