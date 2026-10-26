---
description: Console messages and in-game errors, what causes them and how to fix them.
icon: wrench
---

# Troubleshooting

## Server console

<details>

<summary><code>no supported framework resource is running</code></summary>

`rhd_garage` started before your framework, or no supported framework is installed. Move `ensure rhd_garage` below your framework in `server.cfg`. The same message for `keys`, `fuel`, `target`, `radial` or `notify` should not appear, because each of those has a fallback.

</details>

<details>

<summary><code>unknown fuel provider "..."</code> (or keys, notify, target, radial, framework)</summary>

The id set in `config/main.lua` does not exist. Use one of the ids listed on [Bridges](bridges.md), or `auto`.

</details>

<details>

<summary><code>config/garages.lua entry #3: ...</code></summary>

A garage in `config/garages.lua` is invalid, so the resource stops loading. The message names the entry and the problem, for example `invalid id`, `duplicate id "legion"`, `invalid interaction` or `unknown interior template`. Fix that entry by hand, then restart `rhd_garage`. See the [field reference](garages.md#field-reference).

</details>

<details>

<summary><code>config/garages.lua entry #3 (legion): ..., fix it with /garageadmin</code></summary>

A warning, not an error. The garage loads, but it has no spawn point or preview location, or one of them is outside the zone. Open the garage in `/garageadmin`, fix the points and save.

</details>

<details>

<summary><code>depot garage "depot" is not defined in config/garages.lua</code></summary>

No garage has the id set in `depot.garage` of `config/main.lua`. Create a garage of type `depot` with that id, or change `depot.garage` to the id of your depot.

</details>

<details>

<summary><code>failed to write config/garages.lua</code></summary>

The server cannot write to the resource folder. Check the file permissions of `rhd_garage/config/garages.lua`, and make sure the file is not read-only.

</details>

## In game

| Message | Cause and fix |
| --- | --- |
| You do not have permission | Your player does not have the `admin` ACE. See [Installation](installation.md#grant-admin-access) |
| The spawn area is blocked | A vehicle is standing within `spawn.clearRadius` of every spawn point. Move it, or add more spawn points |
| The vehicle could not be spawned | The vehicle failed to spawn, for example because its model is not streamed on the server. Any depot fee is refunded |
| This vehicle is not available right now | The vehicle is already out in the world, or was moved by another player of a shared garage |
| This vehicle is not registered to anyone | The vehicle you are trying to store is not an owned vehicle |
| You do not own this vehicle | Only the owner can store or take out a vehicle in a `default` garage |
| This vehicle cannot be stored here | The vehicle type is not in the garage's `vehicleTypes` |
| Someone is still inside the vehicle | Every passenger must get out before the vehicle can be stored |
| You must be the driver | Only the driver can store a vehicle |
| You need $... for this | Not enough money in the account set for the depot or the interior |
| Your interior rent has ended | Extend the rent from the garage menu |

## The garage does not appear

* The player is missing the job or gang in `groups`, or their grade is too low.
* The garage was added with [Server Exports](server-exports.md) and the player is not in its `owners`.
* The garage has no `blip`, so it is not on the map. Go to its coordinates to check it.

## Vehicle images do not show

* Add-on vehicles have no image on `docs.fivem.net`. Capture them in the **Images** tab, see [Vehicle Images](vehicle-images.md).
* With local storage, new images appear only after `rhd_garage` restarts.
* Capturing fails with **The screencapture resource is not running** until `screencapture` or `screenshot-basic` is started.
