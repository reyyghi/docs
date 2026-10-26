---
description: Add, update and remove garages at runtime from housing scripts or any other resource.
icon: server
---

# Server Exports

Housing scripts, or any other resource, can add garages at runtime. Runtime garages:

* live in memory only. They are not written to `config/garages.lua` and do not show up in `/garageadmin`.
* are removed automatically when the resource that registered them stops.
* keep their vehicles in the database. Vehicles stored in a runtime garage show up again once the garage is registered again with the same id.

All exports are server side and return `ok, err`: `true` on success, or `false` and an error message.

## RegisterGarage

Adds a garage, or replaces it when `id` is already a runtime garage.

```lua
local ok, err = exports.rhd_garage:RegisterGarage(id, data)
```

* `id`: `string`. Letters, numbers, `_` and `-`, up to 32 characters. Cannot be the id of a garage from `config/garages.lua`.
* `data`: `table`

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `label` | `string` | yes | Up to 48 characters |
| `coords` | `vector4` | yes | Where the player opens the garage. Also the spawn and preview point when `spawn` is not given. `vector3` and `{ x, y, z, w }` are accepted too |
| `owners` | `string[]` | no | Identifiers of the players who receive the garage: `citizenid` on Qbox and QBCore, `identifier` on ESX, `charId` on ox\_core. Leave it out for a garage everyone can use |
| `type` | `string` | no | `default` (each player sees their own vehicles, the default) or `shared` (everyone with access sees every vehicle stored there) |
| `radius` | `number` | no | Zone radius, 1 to 50. Default `5` |
| `spawn` | `vector4[]` | no | Spawn points, all inside `radius`. The first one is also the preview point |
| `spawnSide` | `string` | no | `client` (default) or `server` |
| `interaction` | `string` | no | `keypress` (default), `target`, `radial` or `ped` |
| `ped` | `table` | with `ped` | `{ model = 's_m_y_valet_01', coords = vector4(...) }`, inside `radius` |
| `vehicleTypes` | `string[]` | no | Default `{ 'automobile', 'bike' }` |
| `blip` | `table` | no | `{ sprite = 357, color = 3 }` |
| `groups` | `table` | no | Job or gang with a minimum grade, `{ police = 0 }` |

Runtime garages always use a sphere zone and cannot have an interior.

## SetGarageOwners

Replaces the owner list of a runtime garage, for example when keys are given or taken. Players who lose access stop seeing the garage right away.

```lua
local ok, err = exports.rhd_garage:SetGarageOwners(id, owners)
```

* `id`: `string`
* `owners`: `string[]` or `nil`. `nil` makes the garage public.

## RemoveGarage

Removes a runtime garage.

```lua
local ok, err = exports.rhd_garage:RemoveGarage(id, moveVehiclesTo)
```

* `id`: `string`
* `moveVehiclesTo?`: `string`. Id of another garage. The vehicles stored in the removed garage move there first, and are impounded when it is the depot. Without it, the vehicles keep the removed garage id.

## Example: housing script

{% code title="server.lua" %}
```lua
local function garageId(property)
    return ('house_%s'):format(property.id)
end

local function registerGarage(property)
    local ok, err = exports.rhd_garage:RegisterGarage(garageId(property), {
        label = property.label,
        coords = property.garage, -- vector4
        type = 'shared', -- key holders see each other's vehicles
        owners = { property.owner, table.unpack(property.keyholders) },
    })

    if not ok then
        print(('garage for property %s: %s'):format(property.id, err))
    end
end

-- when a property is bought or loaded
registerGarage(property)

-- when the key holders change
exports.rhd_garage:SetGarageOwners(garageId(property), { property.owner, table.unpack(property.keyholders) })

-- when the property is sold: move its vehicles to the depot, then remove the garage
exports.rhd_garage:RemoveGarage(garageId(property), 'depot')
```
{% endcode %}

Start `rhd_garage` before the housing script, and register the garages again when `rhd_garage` restarts:

```lua
AddEventHandler('onResourceStart', function(resource)
    if resource ~= 'rhd_garage' then return end

    for _, property in pairs(properties) do
        registerGarage(property)
    end
end)
```

## Error messages

| Message | Cause |
| --- | --- |
| `invalid arguments` | `id` is not a string or `data` is not a table |
| `the id is used by a configured garage` | A garage in `config/garages.lua` already uses this id |
| `invalid id` | The id has characters other than letters, numbers, `_` and `-`, or is longer than 32 characters |
| `invalid label` | The label is empty or longer than 48 characters |
| `type must be default or shared` | `type` is not `default` or `shared` |
| `coords must be a vector` | `coords` is missing or not a vector |
| `spawn points must be vectors` | An entry of `spawn` is not a vector |
| `owners must be a list of identifiers` | `owners` is not a list of non-empty strings |
| `radius must be between 1 and 50` | `radius` is out of range |
| `spawn_required` | `spawn` is an empty list. Leave it out to use `coords` instead |
| `spawn_outside_zone` | A spawn point is farther than `radius` from `coords` |
| `ped_outside_zone` | The ped is farther than `radius` from `coords` |
| `ped interaction needs a ped model and vec4 coords` | `interaction = 'ped'` without a valid `ped` table |
| `unknown runtime garage` | No runtime garage with this id |
| `unknown target garage` | `moveVehiclesTo` is not a garage id, or is the garage being removed |
