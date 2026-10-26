---
description: This is an export function to add and remove Model Interactions.
icon: dropbox
---

# Model Interactions

## Add Interactions

```lua
exports.rhd_interact:addModel(model, options)
```

* params:
  * model: `string | string[]`
  * options: `InteractOptions[]`

## Remove Interactions

```lua
exports.rhd_interact:removeModel(model, name)
```

* params:
  * model: `string | string[]`
  * name?: `string | string[]` `option name`

## Example```lua

-- Add Interact
exports.rhd_interact:addModel('prop_dumpster_01a', {
    {
        name = 'rhd_01',
        label = 'Test Aja',
        offset = vec3(0.0, 0.0, 1.0),
        onSelect = function (data)
            print('Option 1 selected')
        end,
        key = 'E',
        groups = {police = {2, 3}}, -- specific grade
        -- groups = {police = 3}, -- minimum grade
        -- groups = {'police', 'ambulance'}, -- job
        distance = 2.0,        -- Interact distance
        pointDistance = 5.0,   -- Point indicator distance
    },
    {
        name = 'rhd_02',
        label = 'Test Aja 2',
        key = 'G',
        offset = vec3(0.0, 0.0, 1.0),
        onSelect = function (data)
            print('Option 2 selected')
        end,
        groups = 'police',
        distance = 4.0,        -- Interact distance
        pointDistance = 5.0,   -- Point indicator distance
    }
})

-- Remove Interact
exports.rhd_interact:removeModel('prop_dumpster_01a', 'rhd_01')
```
