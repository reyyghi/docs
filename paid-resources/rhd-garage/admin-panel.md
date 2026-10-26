---
description: Create garages in-game, manage vehicles, edit interior layouts and capture vehicle images with /garageadmin.
icon: user-shield
---

# Admin Panel

Run `/garageadmin` in game. Access requires the `admin` ACE, see [Installation](installation.md#grant-admin-access).

The panel has four tabs: **Garages**, **Vehicles**, **Interiors** and **Images**. Use **Hide panel** to look around the world while editing, and press `E` to show it again.

Every change made in the panel is printed to the server console with the admin's name, and sent to the ox\_lib logger (`lib.logger`) when one is configured.

## Garages

Select a garage from the list or click **New garage**. The fields match the [field reference](garages.md#field-reference). The **Teleport** button takes you to the garage's coordinates.

### Placing points

**Place** puts the preview location, a spawn point or the ped where you stand, with a ghost vehicle or ped to aim with:

| Key | Action |
| --- | --- |
| `Scroll` | Rotate |
| `Enter` | Confirm |
| `Backspace` | Cancel |

**Use my position** copies your current position without the ghost.

### Drawing zones

* **Sphere**: set the radius.
* **Box**: set width, length, height and rotation. The box is centred on the zone centre. Scroll rotates it while placing.
* **Polygon**: **Draw in world** opens a free camera.

| Key | Action |
| --- | --- |
| `Mouse` | Look around |
| `W` `A` `S` `D` | Move the camera |
| `Q` / `E` | Camera down / up |
| `Shift` | Move faster |
| `Left click` | Add a corner |
| `Right click` / `Backspace` | Remove the last corner |
| `R` / `F` | Raise / lower the next corner |
| `Scroll` | Zone height |
| `Enter` | Save |
| `Esc` | Cancel |

### Saving and deleting

The server checks the garage before saving: spawn points, preview location and ped must be inside the zone, and at least one spawn point is required. The garage is written to `config/garages.lua` and sent to online players right away, without a restart.

Deleting a garage that still holds vehicles asks for confirmation, then moves those vehicles to the depot. The depot garage itself cannot be deleted.

{% hint style="info" %}
Garages added by other resources through [Server Exports](server-exports.md) do not appear in the panel.
{% endhint %}

## Vehicles

Type an exact plate or owner identifier and press `Enter`. Clear the field and press `Enter` to list every vehicle, 20 per page.

| Action | Result |
| --- | --- |
| **Impound** | Deletes the vehicle from the world if it is out, and sends it to the depot |
| **Release to** | Moves the vehicle to the chosen garage. Not possible while the vehicle is out in the world |

## Interiors

Pick a template to preview it or click **Edit layout**. The layout editor teleports you into the interior, where you place the entry point and the display slots. See [Interiors](interiors.md#layout-editor), including **Generate default slot**.

Pick a garage under **Owners and renters** to list the players who bought or rented its interior, and **Revoke** their access.

## Images

Capture vehicle images and choose where they are stored. See [Vehicle Images](vehicle-images.md).
