---
description: This is an export function to add and remove Player Interactions.
icon: user-group
---

# Player Interactions

### Add Interactions

```lua
exports.rhd_interact:addGlobalPlayer(options)
```

* params:
  * options: `InteractOptions[]`&#x20;

### Remove Interactions

```lua
exports.rhd_interact:removeGlobalPlayer(optionName)
```

* params:
  * optionName?: `string | string[]`&#x20;

### Example:

```lua
-- Add Interact
exports.rhd_interact:addGlobalPlayer({
    {
        name = 'trade_player',
        label = 'Trade',
        distance = 2.0,
        pointDistance = 4.0,
        onSelect = function(data)
            local playerName = GetPlayerName(data.playerId)
            print('Trading with player:', playerName, 'ID:', data.playerId)
        end
    },
    {
        name = 'give_item',
        label = 'Give Item',
        distance = 1.5,
        pointDistance = 3.0,
        onSelect = function(data)
            print('Giving item to player ID:', data.playerId)
        end,
        canInteract = function (entity, distance, coords, name, bone)
            return not IsPedInAnyVehicle(entity, false)
        end
    }
})

-- Remove Interact
exports.rhd_interact:removeGlobalPlayer('trade_player')
```
