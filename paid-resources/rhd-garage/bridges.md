---
description: Supported frameworks and resources, how they are detected, and how to connect your own vehicle keys script.
icon: plug
---

# Bridges

RHD Garage talks to your framework and to other resources through bridges. With `auto` (the default), the first resource in the lists below that is started when `rhd_garage` starts is used. To force one, set its id in `config/main.lua`:

{% code title="config/main.lua" %}
```lua
framework = 'qbx',

providers = {
    keys = 'qbx_vehiclekeys',
    fuel = 'ox_fuel',
    notify = 'ox_lib',
    target = 'ox_target',
    radial = 'ox_lib',
},
```
{% endcode %}

An unknown id stops the resource with `unknown <category> provider "<id>"` in the console.

## Framework

| Id | Resource | Vehicle table |
| --- | --- | --- |
| `qbx` | `qbx_core` | `player_vehicles` |
| `ox` | `ox_core` | `vehicles` |
| `esx` | `es_extended` | `owned_vehicles` |
| `qb` | `qb-core` | `player_vehicles` |

Qbox is checked before QBCore because `qbx_core` also provides `qb-core`. Money for the depot and interiors is taken through the framework, which also supplies the player identifier, jobs and gangs.

## Vehicle keys

Keys are given on the server when a vehicle is taken out.

| Id | Resource |
| --- | --- |
| `wasabi_carlock` | `wasabi_carlock` |
| `vehicles_keys` | `vehicles_keys` |
| `qbx_vehiclekeys` | `qbx_vehiclekeys` |
| `qb_vehiclekeys` | `qb-vehiclekeys` |
| `cd_garage` | `cd_garage` |
| `custom` | Your own code, see below. Picked when none of the above is running |

## Fuel

The fuel level is read when a vehicle is stored and applied when it is taken out.

| Id | Resource |
| --- | --- |
| `ox_fuel` | `ox_fuel` |
| `lc_fuel` | `lc_fuel` |
| `cdn_fuel` | `cdn-fuel` |
| `ps_fuel` | `ps-fuel` |
| `legacyfuel` | `LegacyFuel` |
| `native` | GTA fuel level natives. Picked when none of the above is running |

## Target

Used by garages with the `target` and `ped` interactions.

| Id | Resource |
| --- | --- |
| `ox_target` | `ox_target` |
| `qb_target` | `qb-target` |
| `none` | No target. `target` and `ped` garages fall back to the key press |

## Radial menu

Used by garages with the `radial` interaction.

| Id | Resource |
| --- | --- |
| `ox_lib` | `lib.addRadialItem`. Also used with `qbx_radialmenu`, which is built on the ox\_lib radial menu |
| `qb_radialmenu` | `qb-radialmenu` |

## Notify

| Id | Resource |
| --- | --- |
| `wasabi_notify` | `wasabi_notify` |
| `okoknotify` | `okokNotify` |
| `ox_lib` | `lib.notify`. Picked when none of the above is running |

## Custom vehicle keys

To use a keys script that is not listed, edit `bridge/keys/custom.lua` and set `keys = 'custom'`. `give` runs on the server after the vehicle exists:

{% code title="bridge/keys/custom.lua" %}
```lua
---@type KeysProvider
return {
    ---@param source integer player server id
    ---@param entity integer vehicle entity handle on the server
    ---@param plate string vehicle plate
    give = function(source, entity, plate)
        exports.my_keys:GiveKey(source, plate)
    end,
}
```
{% endcode %}

Replace `exports.my_keys:GiveKey` with the export of your keys script. Most scripts take the plate; some, like `qbx_vehiclekeys`, take the entity.
