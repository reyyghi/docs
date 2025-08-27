---
description: This is an export function to add and remove Ped Interactions.
icon: user
---

# Ped Interactions

### Add Interactions

```lua
exports.rhd_interact:addGlobalPed(options)
```

* params:
  * options: `InteractOptions[]`&#x20;

### Remove Interactions

```lua
exports.rhd_interact:removeGlobalPed(optionName)
```

* params:
  * optionName?: `string | string[]`&#x20;

### Example:

```lua
-- Add Interact
exports.rhd_interact:addGlobalPed({
    {
        name = 'talk_to_ped',
        label = 'Talk',
        distance = 2.0,
        pointDistance = 4.0,
        onSelect = function(data)
            print('Talking to ped:', data.entity)
        end,
    },
    {
        name = 'rob_ped',
        label = 'Rob',
        distance = 1.5,
        pointDistance = 3.0,
        onSelect = function(data)
            print('Robbing ped:', data.entity)
        end,
        canInteract = function (entity, distance, coords, name, bone)
            return not IsEntityDead(entity)
        end
    }
})

-- Remove Interact
exports.rhd_interact:removeGlobalPed('talk_to_ped')
```
