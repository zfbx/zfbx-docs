---
description: Change who can use a command
---

# Change Command Permissions

I tried to make all the permissions as fair and even as I could with my experience with servers and staffing, if you disagree with them it's quite easy to change them to suit your needs. There's currently only 3 permission tiers currently (mod, admin and god). Permissions are inherited by a hierarchy so commands with "mod" will also mean "admin" and "god" can access them but a command with "god" will only be usable by someone with the "god" role.

To change the permission for a command find the file the command is in under `server/commands/` and open it in a text editor.&#x20;

Find the line that looks like `role: "mod",` (or `"admin"` or `"god"`) and change it to "mod", "admin" or "god" (whichever you want to be able to run those commands)

Restart zdiscord and that's it! you now have different permission levels for that command.

{% hint style="info" %}
Note that permissions are for a whole file so if you wanted `/money inspect` to be mod and `/money add` to be admin you'd have to either separate the command into another file OR use the **Multiple permissions in a single file** trick below
{% endhint %}

### Multiple permissions in a single file

So you want mods to be able to see people's money (`/money inspect`) but only admins to add, remove and set from it? We're going to use the commands in `money.js` for this example.&#x20;

To modify sub-commands to have a different permission you need to first set the role to the lower level permission for the whole file. In this example that would be `role: "mod"`.&#x20;

Next you'll need to add the following lines to every sub-command you want to be locked behind a higher level role

```javascript
if (!zbot.hasPermission(interaction.member, "admin")) 
    return interaction.sreply(Lang.t("no_permission")).catch(console.error);
}
```

So you'd ignore `if (args.inspect) {` since in this example we want mods to be able to use that and skip down to lines with `if (args.add) {`, `} else if (args.remove) {` and `} else if (args.set) {` and add a new line just under each of them with the snippet above.&#x20;

The snippet above just checks if the person who ran the command has the role ("admin" in this case) and if they don't it stops going any further and replies with the basic reply that a user gets when they try to run a command they don't have permission to run. This message will auto-translate based on the locale set if pasted just like it is above.
