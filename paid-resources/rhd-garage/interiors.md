---
description: Attach GTA Online garage interiors to a garage, sell or rent them, and edit their layouts.
icon: building
---

# Interiors

A garage can have an interior. Players open the garage, buy or rent the interior, and enter it. Inside, they place the vehicles stored in that garage on display slots and pick decoration styles.

## Included templates

| Template id | Interior |
| --- | --- |
| `ceo_arcadius_1` to `ceo_arcadius_3` | Arcadius Business Centre, garages 1 to 3 |
| `ceo_mazebank_1` to `ceo_mazebank_3` | Maze Bank Tower, garages 1 to 3 |
| `ceo_lombank_1` to `ceo_lombank_3` | Lombank West, garages 1 to 3 |
| `ceo_mazebankwest_1` to `ceo_mazebankwest_3` | Maze Bank West, garages 1 to 3 |
| `import_warehouse` | Import/Export Vehicle Warehouse |
| `eclipse_garage` | Eclipse Blvd Garage |
| `auto_shop` | Tuners Auto Shop |
| `agency_garage` | Agency Vehicle Workshop |
| `vinewood_car_club` | Vinewood Car Club |

Templates are defined in `config/interiors.lua`: interior position, IPLs to load or remove, entry point, display slots and decoration groups (entity sets).

{% hint style="warning" %}
DLC interiors only exist when your server runs a game build that includes that DLC. Set `sv_enforceGameBuild` in `server.cfg` to a build that includes the interiors you use.
{% endhint %}

## Interior settings

Set the interior in the garage editor of `/garageadmin`, or in `config/garages.lua`:

{% code title="config/garages.lua" %}
```lua
interior = {
    template = 'auto_shop',
    payment = 'rent',
    price = 5000,
    rentDays = 7,
    perPlayer = true,
    decor = { style = '7' },
},
```
{% endcode %}

| Field | Description |
| --- | --- |
| `template` | Template id from `config/interiors.lua` |
| `payment` | `free`, `purchase` (pay once, owned forever) or `rent` (pay for `rentDays` days) |
| `price` | Whole number. Taken from the account set in `interior.account` of `config/main.lua` |
| `rentDays` | Days added per rent payment, at least 1. Default `7` |
| `perPlayer` | `true` (default): every player gets a private instance with their own decoration. `false`: one shared instance for everyone with access to the garage |
| `decor` | Decoration as `{ [group id] = option id }`. It is the only decoration of a shared instance, and the starting decoration of a private one |

The **Preview** button in the garage editor shows the template with the chosen decoration before you save.

## How players use it

1. Open the garage. The interior panel shows the price and the current status: owned, rented until a date, or ended.
2. **Buy**, **Rent** or **Extend** takes the price from the player's account. Extending adds `rentDays` days to the current end date, or to today when the rent has already ended.
3. **Enter interior** moves the player into the interior, in its own routing bucket.
4. Inside, press `E` at the entry point to open the management panel: decoration (private instances only), display slots, and **Leave interior**.

Rent is never charged automatically. When it ends, the player cannot enter until they extend it. Their decoration and display slots are kept.

## Display slots

Each slot can show one vehicle that the player has stored in this garage. When the vehicle is taken out, its slot is shown empty until the vehicle is stored again.

In a shared instance (`perPlayer = false`) every player sees their own vehicles on the slots.

## Layout editor

The entry point and the display slots belong to the template, so every garage using the same template shares them. Edit them from `/garageadmin` → **Interiors** → **Edit layout**.

**Generate default slot** fills the slots with the positions used in GTA Online:

| Interior | Default slots |
| --- | --- |
| Tuners Auto Shop | 10 |
| Agency Vehicle Workshop | 20 |
| Eclipse Blvd Garage | 10, the same on every floor |
| Import/Export Vehicle Warehouse | 27 floor positions |
| CEO office garages | 20 over 3 floors, taken from Arcadius Business Centre - Garage 1 and rotated to each building |

Generated slots replace the current ones only after you confirm, and are kept only after **Save**.

## Owners and renters

`/garageadmin` → **Interiors** lists the owners and renters of a garage's interior, with the rent end date. **Revoke** removes the record, including the player's decoration and display slots.

## Stuck players

When a player disconnects or crashes inside an interior, or `rhd_garage` restarts while players are inside, they are moved back to the garage the next time their character loads.
