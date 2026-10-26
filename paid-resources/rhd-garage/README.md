---
description: Garage system for Qbox, QBCore, ESX and ox_core with a depot, shared garages, GTA Online interiors and an in-game admin editor.
icon: warehouse
---

# RHD Garage

RHD Garage replaces the default garage of your framework. Players store and take out their vehicles through a full-screen garage menu with vehicle images, condition and handling stats, and a 3D preview. Admins build every garage in-game with `/garageadmin`, without editing coordinates by hand.

## Features

### For players

* Open a garage with a key press, a target, the radial menu or a ped.
* Vehicle cards with images, fuel, engine and body condition, plus speed, acceleration, braking and traction stats.
* 3D preview with an orbit camera, lights, doors and auto rotate.
* Rename vehicles, move them to another garage you can use, and mark favourites.
* Depot for impounded vehicles and vehicles lost in the world, with a retrieval fee per vehicle class.
* Shared garages for jobs and gangs.
* Garage interiors from GTA Online: free, bought or rented, private or shared, with decoration styles and display slots for your stored vehicles.

### For server owners

* In-game admin editor: draw box or polygon zones in the world, place spawn points, the preview location, peds and blips, and restrict garages to jobs or gangs.
* Vehicle search by plate or owner, with impound and release.
* Interior layout editor that can generate the GTA Online display slots.
* Vehicle image studio that captures every vehicle model, including add-ons, and stores the images locally or on Fivemanage.
* Server exports so housing scripts can add private garages at runtime.
* Automatic detection of the framework, vehicle keys, fuel, target, radial and notify resources.

### Performance and security

* The server validates every action: distance to the garage, ownership, vehicle state, and the vehicle model and plate when storing.
* Large payloads travel through latent events, vehicle lists are cached, and the admin vehicle list uses keyset pagination.
* Vehicles left out when the server starts are moved to the depot automatically.

## Requirements

| Resource | Notes |
| --- | --- |
| OneSync | Required |
| [ox\_lib](https://github.com/overextended/ox_lib/releases) | Version 3.x |
| [oxmysql](https://github.com/overextended/oxmysql/releases) | Required |
| Framework | One of `qbx_core`, `qb-core`, `es_extended` or `ox_core` |
| [screencapture](https://github.com/itschip/screencapture) | Optional, only for capturing vehicle images. `screenshot-basic` also works |

## Player controls

While the garage menu is open:

| Key | Action |
| --- | --- |
| `Enter` | Take out the selected vehicle |
| `P` | Preview the selected vehicle |
| `R` | Rename the selected vehicle |
| `T` | Transfer the selected vehicle to another garage (not in the depot) |
| `Q` | Show all vehicles |
| `E` | Show favourite vehicles only |
| `Esc` | Close the menu or leave the preview |

In the preview, right click and drag to orbit the camera and scroll to zoom.

{% hint style="info" %}
Favourites are saved on the player's own client, so they do not follow the player to another PC.
{% endhint %}

## Next steps

{% content-ref url="installation.md" %}
[installation.md](installation.md)
{% endcontent-ref %}

{% content-ref url="garages.md" %}
[garages.md](garages.md)
{% endcontent-ref %}
