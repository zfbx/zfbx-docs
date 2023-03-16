# No handler available for this interaction

If you get a reply on discord stating something like: `No handler available for this interaction (ApplicationCommand > something)`. Then you are most probably also using txadmin and using the same bot token for txadmin as you are for zdiscord which you cannot do.&#x20;

Each bot needs it's own application and token to work properly or they will fight and cause issues. Creating a new bot application for either txadmin or zdiscord OR just disabling the bot on txadmin should fix this issue and make your commands work properly.
