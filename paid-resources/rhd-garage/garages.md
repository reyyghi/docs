---
description: Garage types, interactions, zones, spawn points and every field of config/garages.lua.
icon: square-parking
---

# Garages

Create and edit garages in-game with `/garageadmin` (see [Admin Panel](admin-panel.md)). The editor validates every field and writes the result to `config/garages.lua`. You can also edit that file by hand; changes are loaded when `rhd_garage` restarts.

## Garage types

| Type | Who sees which vehicles |
| --- | --- |
| `default` | Each player sees only their own vehicles stored in this garage |
| `shared` | Everyone with access sees every vehicle stored in this garage, and can take it out. Use it with `groups` for job or gang garages |
| `depot` | Each player sees their impounded vehicles in this depot, plus their vehicles that are out but no longer exist in the world. Taking a vehicle out costs the fee set in `depot.classPrice` |

Vehicles cannot be stored in a depot.

## Interactions

| Interaction | Open the garage | Store a vehicle |
| --- | --- | --- |
| `keypress` | Press `E` inside the zone | Press `E` inside the zone while driving |
| `target` | Target the point at `coords` | Press `E` inside the zone while driving |
| `ped` | Target the ped | Press `E` inside the zone while driving |
| `radial` | Radial menu item with the garage name | Radial menu item **Store vehicle** |

Only the driver can store a vehicle, and every other seat must be empty.

{% hint style="info" %}
When no target resource is running (`target = 'none'`), `target` and `ped` garages fall back to the key press.
{% endhint %}

## Zones

The zone is the area where the garage can be used. Every spawn point, the preview location and the ped must be inside it.

{% tabs %}
{% tab title="Sphere" %}
The default when `zone` is not set: a sphere of `radius` (1 to 50, default 5) around `coords`.

```lua
coords = vec3(-315.75, -888.97, 30.07),
radius = 8.0,
```
{% endtab %}

{% tab title="Box" %}
A box centred on `coords`. `size` is `vec3(width, length, height)`, each between 1 and 100. `rotation` is in degrees.

```lua
coords = vec3(-315.75, -888.97, 30.07),
zone = { type = 'box', size = vec3(14.0, 9.0, 4.0), rotation = 35.0 },
```
{% endtab %}

{% tab title="Polygon" %}
3 to 32 corners. `thickness` is the zone height (1 to 50, default 4). The centre of the polygon becomes `coords`.

```lua
zone = {
    type = 'poly',
    points = {
        vec3(-752.4, -1461.2, 5.0),
        vec3(-738.9, -1459.8, 5.0),
        vec3(-734.6, -1472.5, 5.1),
    },
    thickness = 6.0,
},
```
{% endtab %}
{% endtabs %}

Box and polygon zones are easiest to draw in the world from the admin editor. A zone can reach at most 100 metres from its centre.

## Spawn side

| Value | Behaviour |
| --- | --- |
| `client` | The player's client spawns the vehicle, and the server verifies it before handing it over. The default |
| `server` | The server spawns the vehicle |

On ox\_core vehicles always spawn on the server.

## Field reference

| Field | Required | Description |
| --- | --- | --- |
| `id` | yes | Unique id. Letters, numbers, `_` and `-`, up to 32 characters. Cannot be changed later |
| `label` | yes | Display name, up to 48 characters |
| `type` | yes | `default`, `shared` or `depot` |
| `coords` | yes | `vec3`. Anchor for the blip and the target point. Calculated from the corners for polygon zones |
| `preview` | yes | `vec4`. Where the vehicle is shown during preview. Must be inside the zone |
| `radius` | no | Sphere radius, 1 to 50. Default `5.0` |
| `zone` | no | Box or polygon zone, see [Zones](#zones) |
| `interaction` | no | `keypress` (default), `target`, `radial` or `ped` |
| `ped` | with `ped` | `{ model = 's_m_y_valet_01', coords = vec4(...) }`. Must be inside the zone |
| `vehicleTypes` | no | Vehicle types that can be stored: `automobile`, `bike`, `boat`, `heli`, `plane`, `submarine`, `trailer`, `train`. Default `{ 'automobile', 'bike' }` |
| `spawn.side` | no | `client` (default) or `server` |
| `spawn.points` | yes | List of `vec4` spawn points inside the zone |
| `blip` | no | `{ sprite = 357, color = 3, scale = 0.8 }`. No blip when left out |
| `groups` | no | Job or gang names with a minimum grade, for example `{ police = 0, ballas = 2 }`. Public when left out |
| `interior` | no | Interior settings, see [Interiors](interiors.md) |

{% hint style="warning" %}
A garage without spawn points or without a preview location still loads from the file, but the server console prints a warning. Fix it in `/garageadmin`, which does not save a garage until both are set.
{% endhint %}

## Example

{% code title="config/garages.lua" %}
```lua
return {
    {
        id = 'legion',
        label = 'Legion Square',
        type = 'default',
        coords = vec3(215.8, -810.1, 30.7),
        preview = vec4(229.4, -800.6, 30.5, 160.0),
        radius = 20.0,
        interaction = 'keypress',
        vehicleTypes = { 'automobile', 'bike' },
        spawn = {
            side = 'client',
            points = {
                vec4(222.0, -804.2, 30.6, 248.0),
                vec4(224.4, -799.1, 30.6, 248.0),
            },
        },
        blip = { sprite = 357, color = 3 },
    },
    {
        id = 'mrpd',
        label = 'Police Garage',
        type = 'shared',
        coords = vec3(452.2, -1017.4, 28.5),
        preview = vec4(446.1, -1025.6, 28.6, 0.0),
        radius = 15.0,
        interaction = 'ped',
        ped = { model = 's_m_y_cop_01', coords = vec4(454.1, -1017.4, 28.4, 90.0) },
        spawn = {
            side = 'server',
            points = { vec4(446.1, -1025.6, 28.6, 0.0) },
        },
        groups = { police = 0 },
    },
}
```
{% endcode %}

{% hint style="info" %}
The coordinates above are examples. Place your real points with `/garageadmin` so they are checked against the zone.
{% endhint %}

## Access rules

* A garage with `groups` is sent only to players who have one of those jobs or gangs at the minimum grade or higher. Garages update when the player's job or gang changes.
* Players can transfer their own vehicles only to garages they can use and that accept the vehicle type. The depot is never a target.
* Garages added by other scripts through [Server Exports](server-exports.md) can also be limited to a list of owners.
