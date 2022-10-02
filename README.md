# ULBDiscordBot

[![CodeFactor](https://www.codefactor.io/repository/github/oscarvsp/ulbdiscordbot/badge)](https://www.codefactor.io/repository/github/oscarvsp/ulbdiscordbot)

⚠️ **WORK IN PROGRESS** ⚠️

This is a small discord bot written in python using the [disnake library](https://github.com/DisnakeDev/disnake) to make a registration system for ULB servers.

## 📥 Installation

### Install without docker

```bash
git clone https://github.com/OscarVsp/ULBDiscordBot.git
cd /ULBdDiscordBot
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Install with docker

TODO : Add docker hub link and cmd

## 🤖 Discord Bot

### Creation

Go to the [discord developper portal](https://discord.com/developers/applications):

Create a new application. Once on the app dashboard, go to `Bot` and click `Add Bot`.

### Settings

On the `Bot` page:

Considere unchecking the `Public Bot` field if you don't want everybody to be able to add the bot to their server.

Check the `Server Members Intent`.

You can also change the bot `user name` and `icon`.

Click on `Reset Token` and save the new generated token for later.

On the `OAuth2` `URL Generator` `Scopes`

Check the following fields:

* `bot`
* `applications.commands`

On the `Bot Permissions` that appeared below

Check the following fields:

* `Manages Roles`
* `Manage Nicknames`
* `Send Messages`
* `Use Slash Commands`

Copy the `Generated URL` given below, this is the URL to use to add the bot to your server

## 🔐 Configuration

Copy the `.env_template` -`.env` to easily see all the parameters that need to be set.

### Discord

* `DISCORD_TOKEN`

The bot token generated above.

* `ADMIN_GUILD_ID`

(Optional) The discord server where to register admin commandes (see below)

* `LOG_CHANNEL`

(Optional) The discord channel ID where the bot will send message when an error occure during a command. It need to have acces to this channel. If not provided, the bot owner DM is used.

* `CONTACT_USER_ID`

(Optional) The user id that users can contact in case of an issu with the registration.

* `GUILD_TEMPLATE_URL`

(Optional) The url of the guild template to automatically detect role (must have a `@ULB` role).

### Email

This bot is writen to send email through gmail account.

* `EMAIL_ADDR`

The email address

* `AUTH_TOKEN`

You need to go to the [google account settings Security](https://myaccount.google.com/security?hl=fr), enable the two-factor authentification then generate an applications password for the email app.

### Google Sheet

To generate google sheet api credentials, follow [this guide](https://medium.com/@a.marenkov/how-to-get-credentials-for-google-sheets-456b7e88c430). You will get a `.json` file with all the following fields:

* `GS_TYPE` <- `'type'`
* `GS_PROJECT_ID` <- `'project_id'`
* `GS_PRIVATE_KEY_ID` <- `'private_key_id'`
* `GS_PRIVATE_KEY` <- `'private_key'`
* `GS_CLIENT_EMAIL` <- `'client_email'`
* `GS_CLIENT_ID` <- `'client_id'`
* `GS_AUTHOR_URI` <- `'auth_uri'`
* `GS_TOKEN_URI` <- `'token_uri'`
* `GS_AUTH_PROV` <- `'auth_provider_x509_cert_url'`
* `GS_CLIENT_CERT_URL` <- `'client_x509_cert_url'`

The last field is:

* `GOOGLE_SHEET_URL`

The google sheet url. It need to be shared to the bot using the email address on `client_email`

## 🏃🏼 Run

### Run without docker

```bash
source .venv/bin/activate
python3 main.py
```

### Run with docker

```bash
docker run --env-file=.env ulbdiscordbot
```

## 💠 Bot usage

### ULB servers

* `/setup`

(Admin permission needed) When adding the bot to a new server, you need to setthe @ULB role with the command `/setup`. This commande also allow you to choose if you want to force the registered membre to get rename with real name or not (yes by default).

* `/info`

(Admin permission needed) Get current server information (@ULB role, does rename is enable, and check for permission conflict).

* `/ulb`

Once the ULB role is set, when a new user join the server, either he is already registered (from another of yours server) in which case he will get the `@ULB` role and get rename, or he is not registered yet and will received a DM message with the instruction to register himself using `/ulb` command.

### Admin server

* `/user add`

Manually add an user (don't required email address to be verified)

* `/user info`

Get info about a registered user (discord id, ulb email, name and list of ulb guild that he is on)

* `/user edit`

Edit info of a user.

* `/user delete`

Delete an user.

* `/update`

This force a total update of the database and all the servers. Since the bot already do this automatically at startup and after each disconnection, the only normal usecase for this would be if you manually add an entry (server of user) to the google sheet instead of using the `/user add` command above.
