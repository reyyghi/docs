---
description: This is an export function to add and remove Local Entity Interactions.
icon: code
---

# Local Entity Interactions

### Add Interactions

```lua
exports.rhd_interact:addLocalEntity(entity, options)
```

* params:
  * entity: `number | number[]`&#x20;
  * options: `InteractOptions[]`&#x20;

### Remove Interactions

```lua
exports.rhd_interact:removeLocalEntity(entity, optionName)
```

* params:
  * entity: `number | number[]`&#x20;
  * optionName?: `string | string[]`&#x20;

### Example:

```lua
-- Add Interact
local model = joaat('prop_bin_01a')
local coords = cache.coords
local prop = CreateObject(model, coords.x + 2, coords.y, coords.z, false, false, false)

exports[cache.resource]:addLocalEntity(prop, {
    {
        name = 'move_object',
        label = 'Move Object',
        distance = 1.5,
        pointDistance = 4.0,
        offset = vec(0.0, 0.0, 1.0),
        onSelect = function(data)
            local newCoords = GetEntityCoords(cache.ped)
            SetEntityCoords(data.entity, newCoords.x + 1, newCoords.y, newCoords.z, false, false, false, false)
            print('Moved entity to:', newCoords)
        end
    },
    {
        name = 'delete_entity',
        label = 'Delete Entity',
        distance = 1.5,
        pointDistance = 2.0,
        offset = vec(0.0, 1.0, 1.0),
        onSelect = function(data)
            DeleteEntity(data.entity)
            exports.rhd_interact:removeLocalEntity(data.entity)
            print('Deleted entity:', data.entity)
        end
    }
})

-- Remove Interact
exports.rhd_interact:removeLocalEntity(prop, 'move_object')
```
