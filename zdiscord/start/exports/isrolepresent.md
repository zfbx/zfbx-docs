---
description: check if a user has a discord role
---

# isRolePresent

Returns true or false on if a user has one or many discord roles from their id.&#x20;

### Server Side

#### Parameters

1. **source/id** - Can be either a server id `1-1000` OR a discord id `01234567890123456`
2. **role/roles** - Can be either a single role id or an array of ids

{% tabs %}
{% tab title="Lua Examples" %}
**source with single role:**

<pre class="language-lua"><code class="lang-lua"><strong>local hasRole = exports.zdiscord:isRolePresent(source, "897991948097433681")
</strong></code></pre>



**discord Id with many roles:**

```lua
local hasRole = exports.zdiscord:isRolePresent("142831624868855808", {
    "897991948097433681",
    "897991948097433682"
});
```
{% endtab %}

{% tab title="Javascript Examples" %}
source with single role:

```javascript
const hasRole = global.exports.zdiscord.isRolePresent(global.source, "897991948097433681");
```



discord Id with many roles:

```javascript
const hasRole = global.exports.zdiscord.isRolePresent("142831624868855808", [
    "897991948097433681",
    "897991948097433682"
]);
```
{% endtab %}
{% endtabs %}

### Client Side

From client you can check if the current user has roles. (Lua only)

{% hint style="info" %}
While you can do this from the client, you should never trust the client to check it's own permissions for moderation or monetary functionality as there's always a chance it could be exploited
{% endhint %}

**Single role example:**

```lua
local hasRole = exports.zdiscord:isRolePresent("897991948097433681")
```

**Multiple roles example:**

```lua
local hasRole = exports.zdiscord:isRolePresent({
    "897991948097433681",
    "897991948097433682"
});
```

