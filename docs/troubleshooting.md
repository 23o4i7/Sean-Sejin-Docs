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
| Error contains `ZodError` | The `.setName()` value in one of your commands contains a non-letter or non-lowercase character. | Double check the names of all your commands in the `.setName()` field to make sure you only have lowercase letters as your command name. |