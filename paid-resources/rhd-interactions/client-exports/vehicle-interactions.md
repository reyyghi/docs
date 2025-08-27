---
description: This is an export function to add and remove Vehicle Interactions.
icon: car
---

# Vehicle Interactions

### Add Interactions

```lua
exports.rhd_interact:addGlobalVehicle(options)
```

* params:
  * options: `InteractOptions[]`&#x20;

### Remove Interactions

```lua
exports.rhd_interact:removeGlobalVehicle(optionName)
```

* params:
  * optionName?: `string | string[]`&#x20;

### Example:

```lua
-- Add Interact
exports.rhd_interact:addGlobalVehicle({
    {
        name = 'engine_repair',
        label = 'Repair Engine',
        bones = 'bonnet',
        distance = 2.0,
        pointDistance = 5.0,
        onSelect = function(data)
            print('Repairing engine of vehicle:', data.entity)
        end
    },
    {
        name = 'open_hood',
        label = 'Open Hood',
        bones = 'bonnet',
        distance = 1.5,
        onSelect = function(data)
            SetVehicleDoorOpen(data.entity, 4, false, false) -- Hood
        end
    }
})

-- Remove Interact
exports.rhd_interact:removeGlobalVehicle('engine_repair')
```
