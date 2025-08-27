---
description: This is an export function to add and remove Networked Entity Interactions.
icon: code
---

# Networked Entity Interactions

### Add Interactions

```lua
exports.rhd_interact:addEntity(netId, options)
```

* params:
  * netId: `number | number[]`&#x20;
  * options: `InteractOptions[]`&#x20;

### Remove Interactions

```lua
exports.rhd_interact:removeEntity(netId, optionName)
```

* params:
  * netId: `number | number[]`&#x20;
  * optionName?: `string | string[]`&#x20;

### Example:

*   #### Server Side



    ```lua
    RegisterCommand('createEntity', function (source, args)
        local model = joaat(args[1] or 'prop_dumpster_01a')
        local playerPed = GetPlayerPed(source)
        local coords = GetEntityCoords(playerPed)

        local entity = CreateObjectNoOffset(model, coords.x + 2, coords.y, coords.z, true, false, false)
        Wait(100)

        if not DoesEntityExist(entity) then
            print('Failed to create entity with model:', model)
            return
        end

        local netId = NetworkGetNetworkIdFromEntity(entity)

        local players = exports.rhd_fivem:getPlayersInScope(source)
        if not players then return end

        lib.triggerClientEvent('createInteract', players, netId)
    end, false)
    ```



*   #### Client Side 

    ```lua
    local created = {}

    RegisterNetEvent('createInteract', function(netId)
        if created[netId] then
            return
        end

        exports.rhd_interact:addEntity(netId, {
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
                name = 'delete_cone',
                label = 'Delete Cone',
                distance = 1.5,
                pointDistance = 2.0,
                offset = vec(0.0, 1.0, 1.0),
                onSelect = function(data)
                    created[netId] = nil
                    DeleteEntity(data.entity)
                    exports.rhd_interact:removeEntity(netId)
                    print('Deleted entity:', data.entity)
                end
            }
        })
    end)
    ```
