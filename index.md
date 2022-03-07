---
layout: default
title: Introduction
nav_order: 1
---

# Introduction
{: .no_toc }
The purpose of this document is to guide beginners on Discord how to create a Discord Bot. The sections of this document will introduce you to the simplest and easiest way to create your own Discord Bot.

A Discord Bot is created by a user with a developer account to automate various actions on Discord. Discord’s public API is used to make Bots take some actions. The features of each bot are various by its creator or user, but there are certain basic roles that are shared among the bots, such as sending messages, modifying roles, communicating with other servers, and etc.

## Intended Users
This document is targeted towards to any beginner developers who want to create a bot using Discord's API. Bots can be used to interact with a server or community by greeting and orienting new users, moderating discussions, or use third-party functions such as play music or games with users.

## Procedures Overview
The main sections of the documentation are as follows:

* Create a Discord Developer Account
* Register a New Bot on Discord
* Authorize and Connect Your Bot to a Server
* Initalize Your Bot
* Running Your Bot

## Prerequisites
To follow each step of the process, you need the following:

  * Access to a computer
  * Secure internet connection
  * Working knowledge of Javascript and Node.js
  * Basic understanding of [async and await](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await) functions in Javascript

## Software Requirements
Before proceeding, ensure you have the following installed:

  * Node.js V16.9.0+ ([Download](https://nodejs.org/en/))
  * An Integrated Development Environment (IDE)
    * [Visual Studio Code (Recommended)](https://code.visualstudio.com/download), [WebStorm](https://www.jetbrains.com/webstorm/download/), [Atom](https://atom.io/), [Eclipse](https://www.eclipse.org/downloads/packages/), [Notepad++ (Not recommended)](https://notepad-plus-plus.org/downloads/)
  * Any up-to-date browser
    * [Google Chrome](https://www.google.com/intl/en_ca/chrome/), [Firefox 38+](https://www.mozilla.org/en-CA/firefox/products/), [Opera](https://www.opera.com/), [Microsoft Edge 17+](https://www.microsoft.com/en-us/edge), [Safari 11+](https://support.apple.com/downloads/safari), or [Chromium 79+](https://www.chromium.org/chromium-projects/)

## Typographical Conventions

| Convention   | Appearance  | Examples |
|:-------------|:------------|:---------|
| Important Items and Emphasis | ***Bold Italics*** | ***user, console, instructions*** |
| Key Press | **Bold** | **Ctrl+Shift+C, Alt+A, Enter** |
| Links | [Link]() | [This is a Link](https://23o4i7.github.io/Sean-Sejin-Docs/) |
| Code Input | `code` | ```console.log("Hello World)``` |
| Console Output | _`code italics`_ | _`console.log("Hello World")`_ |
| Warning | ![warning](./graphics/warning.png) | ![warning](./graphics/warning2.png) |
| Important Note | ![note](./graphics/important.png) | ![note](./graphics/important2.png) |