---
description: How to set up electric vehicles in rhd_fuel.
icon: charging-station
---

# Electric Vehicles

{% stepper %}
{% step %}
### Add the models

{% hint style="info" %}
Only needed on a game build below 3258.
{% endhint %}

Open `config/electric.lua` and add the electric vehicle models to the `vehicleModels` table:

```lua
vehicleModels = {
    "surge",
    "iwagen",
    "voltic",
    "voltic2",
    "raiden",
    "cyclone",
    "tezeract",
    "neon",
    "omnisegt",
    "caddy",
    "caddy2",
    "caddy3",
    "airtug",
    "rcbandito",
    "imorgon",
    "dilettante",
    "khamelion",
}
```
{% endstep %}

{% step %}
### Change `strHandlingFlags` in `handling.meta`

In the `handling.meta` of each electric vehicle, set `strHandlingFlags` to `1000`:

```xml
<strHandlingFlags value="1000" />
```
{% endstep %}
{% endstepper %}
