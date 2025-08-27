---
description: This is an export function to add and remove Coords Interactions.
icon: map-pin
---

# Coords Interactions

### Add Interactions

```lua
exports.rhd_interact:addCoords(CoordsProps)
```

* params:
  * id?: `string`&#x20;
  * coords: `vector3`&#x20;
  * options: `InteractOptions[]`&#x20;
* return: `string` `coordsId`&#x20;

### Remove Interactions

```lua
exports.rhd_interact:removeCoords(coordsId, optionName)
```

* params:
  * coordsId: `string`&#x20;
  * optionName?: `string | string[]`&#x20;

### Example:

```lua
-- Add Interact
local id = exports.rhd_interact:addCoords({
    id = 'test_location_1',
    coords = vec3(cache.coords.x, cache.coords.y, cache.coords.z),
    options = {
        {
            name = 'teleport_here',
            label = 'Teleport Here',
            distance = 2.0,
            pointDistance = 5.0,
            onSelect = function(data)
                SetEntityCoords(cache.ped, data.coords.x, data.coords.y, data.coords.z + 1, false, false, false, false)
            end
        },
        {
            name = 'mark_location',
            label = 'Mark Location',
            distance = 1.5,
            pointDistance = 3.0,
            onSelect = function(data)
                print('Marked location:', data.coordsId, 'at coords:', data.coords)
            end
        }
    }
})

-- Remove Interact
exports.rhd_interact:removeCoords(id, 'teleport_here')
```
