---
description: Every option in config/main.lua explained.
icon: sliders
---

# Configuration

RHD Garage has three config files:

| File | Content |
| --- | --- |
| `config/main.lua` | General settings, explained on this page |
| `config/garages.lua` | Garage definitions. Written by `/garageadmin`, see [Garages](garages.md) |
| `config/interiors.lua` | Interior templates. Layouts are written by `/garageadmin`, see [Interiors](interiors.md) |

Restart `rhd_garage` after editing a config file by hand.

## Framework and providers

```lua
framework = 'auto',

providers = {
    keys = 'auto',
    fuel = 'auto',
    notify = 'auto',
    target = 'auto',
    radial = 'auto',
},
```

`auto` picks the first supported resource that is started. Set a provider id to force one, for example `fuel = 'ox_fuel'`. The ids and the detection order are listed on [Bridges](bridges.md).

## Interaction key

```lua
interactKey = 38,
```

The [control index](https://docs.fivem.net/docs/game-references/controls/) used to open or store at garages with the `keypress` interaction. `38` is `E`.

{% hint style="info" %}
The help text in `locales/*.json` (`help_open`, `help_store`, `help_interior`) shows `~INPUT_PICKUP~`, which is `E`. Update those strings if you change the key.
{% endhint %}

## Depot

```lua
depot = {
    garage = 'depot',
    account = 'cash',
    defaultPrice = 500,
    classPrice = {
        [0] = 300, -- Compacts
        [1] = 500, -- Sedans
        -- ...
        [22] = 2500, -- Open Wheel
    },
},
```

| Option | Description |
| --- | --- |
| `garage` | Id of the depot garage in `config/garages.lua`. Impounded vehicles, vehicles of a deleted garage, and vehicles left out at server start are sent here |
| `account` | `cash` or `bank`. The account the retrieval fee is taken from |
| `classPrice` | Retrieval fee per vehicle class (`GetVehicleClass`, `0` to `22`) |
| `defaultPrice` | Fee for a vehicle whose class is unknown |

The fee is refunded when the vehicle fails to spawn.

## Spawning

```lua
spawn = {
    clearRadius = 3.0, -- meter
    confirmTimeout = 15000, -- ms
},
```

| Option | Description |
| --- | --- |
| `clearRadius` | A spawn point is used only when no vehicle is within this distance. The first free point is used |
| `confirmTimeout` | With client side spawning, how long the server waits for the player's client to confirm the spawned vehicle. Without a confirmation the take out fails and the depot fee is refunded |

## Cache

```lua
cache = {
    vehicleTtl = 60, -- seconds
},
```

How long a vehicle list stays in server memory. Writes made by RHD Garage update the cache in place. Taking out and storing a vehicle always read the database row again, so changes saved by other scripts (tuning, mechanic or plate scripts) are kept.

## Ped

```lua
ped = {
    renderDistance = 50.0, -- meter
},
```

Garages with the `ped` interaction spawn their ped only when the player is within this distance.

## Preview

```lua
preview = {
    depthOfField = true,
    autoRotate = false,
},
```

| Option | Description |
| --- | --- |
| `depthOfField` | Blur the background during the vehicle preview |
| `autoRotate` | Start the preview with auto rotate on. Players can still toggle it |

## Interior

```lua
interior = {
    account = 'bank',
    bucketOffset = 7000,
    slotPreviewModel = 'sultan',
},
```

| Option | Description |
| --- | --- |
| `account` | `cash` or `bank`. Used to buy or rent interiors |
| `bucketOffset` | First routing bucket used by interiors. RHD Garage uses buckets from this number up to `bucketOffset + 9000` plus the highest player id. Pick a range no other script uses |
| `slotPreviewModel` | Vehicle model placed on every display slot while an admin edits or previews an interior layout |

## Vehicle names

```lua
vehicleName = {
    maxLength = 24,
},
```

Maximum length of a custom vehicle name.

## Vehicle images

```lua
vehicleImages = {
    'https://docs.fivem.net/vehicles/%s.webp',
},
```

The default image URL templates, tried in order when a model has no captured image. `%s` becomes the model name. Once an admin saves the list in the **Images** tab of `/garageadmin`, that saved list is used instead. See [Vehicle Images](vehicle-images.md).

## Capture studio

```lua
capture = {
    studio = vec3(-1700.0, -4200.0, 900.0),
    angle = 35.0, -- degrees from the front
    pitch = 8.0, -- degrees
    fov = 30.0,
    fill = 0.86, -- 0-1 of the frame
    settle = 600, -- ms
    swapFrames = 10,
    hour = 12,
    weather = 'EXTRASUNNY',
    backdrops = {
        { 0, 102, 0 },
        { 255, 0, 255 },
    },
    lights = {
        { side = 1.2, front = 1.4, up = 1.0, intensity = 4.0 },
        -- ...
    },
    maxUploads = 3,
},
```

| Option | Description |
| --- | --- |
| `studio` | Where the vehicle is placed while it is captured. Keep it far from the map, above the ocean |
| `angle`, `pitch` | Camera angle around the vehicle and above it, in degrees |
| `fov` | Camera field of view |
| `fill` | How much of the frame the vehicle fills, from `0` to `1` |
| `settle` | Wait time after the vehicle spawns, before the first shot |
| `swapFrames` | Frames to wait after the backdrop changes |
| `hour`, `weather` | Time and weather while capturing |
| `backdrops` | The two backdrop colours (RGB). Both must have equal brightness |
| `lights` | Studio lights, positioned relative to the vehicle size |
| `maxUploads` | Number of images uploaded to the server at the same time |

The defaults work for most servers. Change them only if your images look wrong.
