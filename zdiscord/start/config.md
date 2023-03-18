---
description: Basic walkthrough of config.js options and convars
---

# 🪛 Configure

Here I will break down all the configuration options in the `config.js`. I will also be including examples and list which config options have convar[^1] alternatives.

<details>

<summary>GENERAL SETTINGS</summary>

#### Language

**\[ Default: "en" | Convar: `zdiscord:Language` ]** This determines which locale (translation) file is loaded from `/locales` so if the file that fits the language you want used is in that folder then use the 2 character name of the file. As of writing this ar, de, en, pl, tr and vn are available options.

### LanguageWarnings

#### FivemName

**\[ Replicated | Convar: `zdiscord:FivemName` ]** This is what you want your FiveM server to be called, this value is used in various places as an auto-fill like bot status and commands as well as translations when people are connecting to your server.

#### Invite

**\[ Replicated | Convar: `zdiscord:Invite` ]** A link to your discord server that will be given to users on connection problems to the FiveM server, used for discord presence links and some command replies.

#### FivemUrl

**\[ Replicated | Convar: `zdiscord:FivemUrl` ]**

#### Verbose Logging

**\[ Convar: `zdiscord:VerboseLogging` ]** Turns on more verbose logging telling you what's loading or not

#### Debug Logging

**\[ Convar: `zdiscord:DebugLogging` ]** Turns on debug logging from discord.js for checking for errors

</details>

<details>

<summary>DISCORD BOT SETTINGS</summary>

#### Enabled

**\[ Convar: `zdiscord:Enabled`]**\
This option deterrmins whether the bot actually connects to discord at all. if this is set to false the bot portions will not work at all. but log webhooks, presence updates and connection queue will continue though without priority

#### BotToken

**\[ Convar: `zdiscord:BotToken`]**\
This is where you put your discord bot token generated from [Discord Applications](https://discord.com/developers/applications). It will look somewhat like `ZDkx5NjQxjExNMzDM1D2U0O4.v9g7Wa.DK700Xi2LeVOC2NUuABgPt0ZyWR`.\
**DO NOT** Share this token with anyone, it's a key to your bot and discord server which could be dangerous in the wrong hands.

#### ServerId

**\[ Convar: `zdiscord:ServerId` ]**\
This is for your Discord Server id (Also called a Guild Id). You can get that by enabling developer mode in your discord client then right clicking your discord server icon and "copy id". This is an important value, the bot will only listen to events done within this server.

#### SlashCommandsEnabled

**\[ Convar: `zdiscord:SlashCommandsEnabled` ]**\
If this is set to `"true"` the bot will register all it's slash commands to the discord server and allow users with the correct roles to access them. if this is set to `"false"` all the commands will ignored and never registered.

#### ModRoleIds

**\[ Convar: `zdiscord:ModRoleIds` ]**\
This is an array of discord role IDs that will be permitted to use commands set to role `"mod"`. this can only be a single role unlike WhitelistRoleIds. You can add other roles but you'll have to follow the [guide](https://zfbx.github.io/zdiscord/commands#add-permission-levels). You can get the role ID in the same way described under WhitelistRoleIds

#### AdminRoleIds

**\[ Convar: `zdiscord:AdminRoleIds` ]**\
This is an array of discord role IDs that will be permitted to use commands set to role `"admin"` OR `"mod"`. Otherwise refer to ModRoleIds's notes.

#### GodRoleIds

**\[ Convar: `zdiscord:GodRoleIds` ]**\
This is an array of discord role IDs that will be permitted to use **all** commands. Including `"admin"` and `"mod"`. Otherwise refer to ModRoleIds's notes.

#### StatusMessages

**\[ Convar: `zdiscord:StatusMessages` ]**\
The bot will pick a random message from this array every 30 seconds to set as it's status. You can use `{playercount}`, `{servername}` or `{invite}` inside the status messages and when they're shown they will replace those values with either the current number of players online, the server name set under FivemName or invite set under Invite.

</details>

<details>

<summary>STAFF CHAT SETTINGS</summary>

#### StaffChatEnabled

**\[ Convar: `zdiscord:StaffChatEnabled`]**\
This set to "true" will enable the feature of forwarding chat from in game to discord and back in the channel configured in the next setting.

#### StaffChatChannelId

**\[ Convar: `zdiscord:StaffChatChannelId` ]**\
This is the channel staff chat will be sent and be taken from to send to staff in game. this can only be 1 channel and some things might not look the same in game as they do in discord like emoji or @mentions but that's normal.

#### AdditionalStaffChatRoleIds

if you have extra roles you'd like to access staff chat other than the default mod, admin and god roles configured below you can add other roles here and they'll have access to see and toggle staff chat. Just make sure they can also see the StaffChatChannelId channel ;)

</details>

<details>

<summary>WHITELIST SETTINGS</summary>

#### WhitelistEnabled

**\[ Convar: `zdiscord:WhitelistEnabled` ]**\
This setting determines whether the bot should check if someone is in the discord and if they have a preset role defined under WhitelistRoleIds. Setting this to `"true"` wont let anyone into the server unless they:

1. Have Discord open.
2. Are in the Discord defined in ServerId.
3. Have the whitelisted role in the discord

#### WhitelistRoleIds

**\[ Convar: `zdiscord:WhitelistRoleIds` ]**\
This is an array of ids (`[ "role1id", "role2id", "role3id" ]`) of role IDs that will be able to connect to the server if WhitelistEnabled is set to "true". To get a role Id you enable developer mode in your discord client then either right click a role name from someone's popup profile or right click the role name in the role settings and "copy id".

</details>

<details>

<summary>ACE PERMISSION SETTINGS</summary>

#### AcePermsEnabled

**\[ Convar: `zdiscord:AcePermsEnabled` ]**\
If this is set to `"true"` it'll enable a system of granting users Ace Permissions based on their role configured under AutoAcePermissions.

**NOTE: This will only work if `add_ace resource.zdiscord command allow` is set in the server.cfg**

#### AutoAcePermissions

If AcePermsEnabled is set to `"true"` the configured ace permissions will be automatically given to users which have at least one of the matching roles. For example if you put `"group.police": "DiscordPoliceRoleID",` as one of the rows, if a user joined the server and had the `DiscordPoliceRoleID` in discord the bot will automatically set the `group.police` ace permission to them. On disconnect all ace permissions granted are removed.

By default the discord mod, admin and god roles are given `group.mod`, `group.admin` or `group.god` respectively.

Set a single role id with `"example": "000000000000000000",`. You can also have multiple discord roles checked for an Ace permission by using an array instead of a single roleId string like: `"example2": [ "000000000000000000", "000000000000000000"],`

**NOTE: This will only work if `add_ace resource.zdiscord command allow` is set in the server.cfg**

</details>

<details>

<summary>WEBHOOK SETTINGS</summary>

#### WebhooksEnabled

**\[ Convar: `zdiscord:WebhooksEnabled` ]**\
This setting enables the abilty to use the log export. if this is set to false the export will return false and not send the event.

#### WebhooksName

**\[ Convar: `zdiscord:WebhooksName` ]**\
This is the name to display in discord when the logs come through. Webhooks work slightly different from the normal bot and can have their own names or pictures set without issue, these "bots" however can't read messages or show up in the user list, it's just a one way message

#### WebhooksPing

**\[ Convar: `zdiscord:WebhooksPing` ]**\
This discord id will be pingged in the event a log is sent with `true` for pingRole. This can be used to give attention to an important log that a dedicated staff team might want to know about or deal with for example a monetary transaction over a certain amount might be suspicious and warrent a ping to this user or role. There can only be one id for this.\
**IMPORTANT NOTE:** If you want to ping a user just put the ID, if you want to **ping a role** put a `&` in front of the role id\*\*

#### LoggingWebhooks

This is the array of webhooks you setup to be used with the log system. it uses `"key": "value",` where `key` is the name (case sensitive) of the webhook for you to be able to call from the logging export as the first value

</details>

<details>

<summary>SCRIPT EVENT SETTINGS</summary>

clothing menu

revive player event

use notity instead of chat

</details>

<details>

<summary>OTHER SETTINGS</summary>

#### SaveScreenshotsToServer

**\[ Convar: `zdiscord:SaveScreenshotsToServer` ]**\
If you want discord `/screenshot`s to be saved locally to the server set this to `"true"` however if you just want the screenshots to be sent to discord when the command is used leave this as `"false"`. Please note if you change this to true, it's up to you to monitor your screenshots folder as images can be quite large and use a lot of space if they don't get cleaned up regularly.

vehicleStates

teleport locations

</details>

### What are convars?

Convars ([see docs](https://docs.fivem.net/docs/scripting-reference/convars/#standard-convars)) are settings that you set inside your server.cfg outside of the resource. this makes it really easy to drop in/update a resource's files easily and not worry so much about the config settings or secret values getting out. In your server's cfg file before you `ensure zdiscord` you can add settings there like this instead of setting them in the `config.js`:

```lua
set zdiscord:BotToken "MJHgjhgJhglNjA3sdM.GXsdfC.3isdfgsdggs2ksdfgsdfgsdfgUFs"
set zdiscord:ServerId "354143016996569089"
set zdiscord:ModRoleIds "1086316532310745129"
set zdiscord:AdminRoleIds "1086316710774181999"
set zdiscord:GodRoleIds "1086316489478512702"
set zdiscord:WhitelistEnabled true
set zdiscord:WhitelistRoleIds [ "1086316576011198526", "1086316576011198527" ]
ensure zdiscord
```



[^1]: Explained at bottom of this page.
