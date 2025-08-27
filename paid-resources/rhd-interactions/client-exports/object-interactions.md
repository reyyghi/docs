---
description: This is an export function to add and remove Object Interactions.
icon: boxes-stacked
---

# Object Interactions

### Add Interactions

```lua
exports.rhd_interact:addGlobalObject(options)
```

* params:
  * options: `InteractOptions[]`&#x20;

### Remove Interactions

```lua
exports.rhd_interact:removeGlobalObject(optionName)
```

* params:
  * optionName?: `string | string[]`&#x20;

### Example:

```lua
-- Add Interact
exports.rhd_interact:addGlobalObject({
    {
        name = 'pickup_object',
        label = 'Pick Up',
        distance = 1.5,
        pointDistance = 3.0,
        onSelect = function(data)
            print('Picking up object:', data.entity)
        end
    },
    {
        name = 'examine_object',
        label = 'Examine',
        distance = 2.0,
        pointDistance = 4.0,
        onSelect = function(data)
            print('Examining object:', data.entity, 'Model:', GetEntityModel(data.entity))
        end
    }
})

-- Remove Interact
exports.rhd_interact:removeGlobalObject('pickup_object')
```
