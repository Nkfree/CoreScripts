# Creating Commands

To create a chat command, simply run this function on startup:
* `customCommandHooks.registerCommand(cmd, callback)`  
  `cmd` is the word after `/` which you want to trigger your command (e.g. "help" for `/help`)  
  `callback` is a function which will be ran when someone sends a message starting "/`cmd`"

Callback will receive as its arguments a player's `pid` and a table of all command parts (their message is split into parts by spaces, after removing the leading '/', same as in the old `commandHandler.lua`).

You can limit which players can run the command with the following functions:
* `customCommandHooks.setRankRequirement(cmd, rank)`  
  where `rank` is the same as in `Players[pid].data.settings.staffRank`
* `customCommandHooks.removeRankRequirement(cmd)`
* `customCommandHooks.setNameRequirement(cmd, names)`  
  where `names` is a table of player `accountName`s
* `customCommandHooks.addNameRequirement(cmd, name)`  
  where `name` is a player's `accountName`
* `customCommandHooks.removeNameRequirement(cmd)`

You can also perform more advanced checks inside the callback by calling `Players[pid]:IsAdmin()` and other similar functions.

# Examples:

```Lua
    customCommandHooks.registerCommand("test", function(pid, cmd)
        tes3mp.SendMessage(pid, "You can execute a normal command!\n", false)
    end)

    customCommandHooks.registerCommand("ranktest", function(pid, cmd)
        tes3mp.SendMessage(pid, "You can execute a rankchecked command!\n", false)
    end)
    customCommandHooks.setRankRequirement("ranktest", 2) -- must be an Admin


    customCommandHooks.registerCommand("nametest", function(pid, cmd)
        tes3mp.SendMessage(pid, "You can execute a namechecked command!\n", false)
    end)
    customCommandHooks.setNameRequirement("nametest", {"Admin", "Kneg", "Jiub"})
```
