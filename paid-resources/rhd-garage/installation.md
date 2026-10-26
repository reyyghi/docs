---
description: Install RHD Garage, grant admin access and create your first garage.
icon: download
---

# Installation

{% stepper %}
{% step %}
### Place the resource

Extract `rhd_garage` into your resources folder, for example `resources/[rhd]/rhd_garage`.

Do not run another garage script at the same time. Two garage scripts would change the same vehicle rows in your database.
{% endstep %}

{% step %}
### Add it to `server.cfg`

Start `rhd_garage` **after** oxmysql, ox\_lib, your framework, and your keys, fuel, target, radial and notify resources. Providers set to `auto` are detected when `rhd_garage` starts, so a resource that starts later is not picked up.

{% code title="server.cfg" %}
```cfg
ensure oxmysql
ensure ox_lib
ensure qbx_core        # or qb-core, es_extended, ox_core

# keys, fuel, target, radial and notify resources go here

ensure rhd_garage
```
{% endcode %}
{% endstep %}

{% step %}
### Grant admin access

The admin panel (`/garageadmin`) checks the `admin` ACE. Grant it to your admin group and add your admins to that group:

{% code title="server.cfg" %}
```cfg
add_ace group.admin admin allow
add_principal identifier.fivem:1234567 group.admin
```
{% endcode %}
{% endstep %}

{% step %}
### Choose the language (optional)

RHD Garage ships with English (`en`) and Indonesian (`id`). The language follows the ox\_lib locale convar:

{% code title="server.cfg" %}
```cfg
setr ox:locale "en"
```
{% endcode %}

Translations live in `locales/*.json`. Copy `en.json` to add a new language.
{% endstep %}

{% step %}
### Start the server

On the first start RHD Garage creates its own tables:

| Table | Content |
| --- | --- |
| `rhd_garage_vehicles` | Custom vehicle names and cached vehicle types |
| `rhd_garage_interiors` | Interior owners, rent end dates, decoration and display slots |
| `rhd_garage_images` | Captured vehicle images |

On ESX, the `parking` and `pound` columns are added to `owned_vehicles` when they are missing. No SQL file has to be imported by hand.
{% endstep %}

{% step %}
### Create your garages

Join the server and run `/garageadmin`. The default `config/garages.lua` contains one example garage and the depot (`id = "depot"`). Edit them or create new ones, see [Admin Panel](admin-panel.md) and [Garages](garages.md).

{% hint style="warning" %}
Keep a garage with the id set in `depot.garage` (default `depot`). Impounded vehicles and vehicles left out at server start go there.
{% endhint %}
{% endstep %}
{% endstepper %}

## Updating from v1

* Custom vehicle names from v1 (`custom_veh_name`) are copied to `rhd_garage_vehicles` on the first start. The old column is left untouched.
* Garage locations from v1 (`config/location.lua`) are not imported. Create them again with `/garageadmin`.
* Replace the whole resource folder. Do not copy v1 config files into v2.

## Building the UI (optional)

The compiled UI in `web/build` is included. Rebuild it only if you change the source in `web/src`:

```bash
cd web
npm ci
npm run build
```
