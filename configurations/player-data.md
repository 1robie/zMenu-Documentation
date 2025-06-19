---
description: Player data system
---

# 🛝 Player data

With zMenu you can store data for the player and use it with placeholders. This way you can create counters, cooldowns and much more !

Each data contains a key, a value and an expiration date. If you put **0** then the data will never expire. The expiration date is a timestamp.

## Commands

The permission to use these commands is: `zmenu.players`

<table><thead><tr><th width="410">Command</th><th>Description</th></tr></thead><tbody><tr><td>/zm players</td><td>Displays the list of commands for the players' data.</td></tr><tr><td>/zm players set &#x3C;player> &#x3C;key> &#x3C;expiration> &#x3C;value></td><td>Set new player data. You must set the expiration time in seconds. Put 0 to have no expiration.</td></tr><tr><td>/zm players remove &#x3C;player> &#x3C;key></td><td>Remove player data.</td></tr><tr><td>/zm players get &#x3C;player> &#x3C;key></td><td>Get player data.</td></tr><tr><td>/zm players kets &#x3C;player></td><td>Returns the list of keys of a player.</td></tr><tr><td>/zm players clear &#x3C;player></td><td>Clear player's data.</td></tr><tr><td>/zm players clearall</td><td>Clear all player's data.</td></tr><tr><td>/zm players add &#x3C;player> &#x3C;key> &#x3C;value></td><td>Add a number to a value, works only for numbers.</td></tr><tr><td>/zm players subtract &#x3C;player> &#x3C;key> &#x3C;value></td><td>Subtract a number to a value, works only for numbers.</td></tr></tbody></table>

## Placeholders

Placeholders can be used in an inventory for displaying an item or for a permission. You can block access to a button with a placeholder. You can see an example [here](broken-reference).

<table><thead><tr><th width="426.56591923371104">Placeholder</th><th>Description</th></tr></thead><tbody><tr><td><code>%zmenu_player_value_&#x3C;key>%</code></td><td>Returns the value contained in a key. </td></tr><tr><td><code>%zmenu_player_expire_format_&#x3C;key>%</code></td><td>Returns the expiration time formatted according to a key.</td></tr><tr><td><code>%zmenu_player_expire_&#x3C;key>%</code></td><td>Returns the expiration time according to a key.</td></tr><tr><td><code>%zmenu_player_key_exist_&#x3C;key>%</code></td><td>Returns true or false. Allows to know if a key exists.</td></tr></tbody></table>
