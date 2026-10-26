---
description: Pizza delivery activity created by the RHD team, inspired by GTA5 Online
icon: pizza-slice
---

# RHD Pizza Delivery

## Installation

{% stepper %}
{% step %}
Open the `config.lua` file and configure it to your liking.
{% endstep %}

{% step %}
Then, start in `server.cfg` like the code below:

{% code title="server.cfg" %}
```cfg
ensure ox_lib
ensure es_extended
ensure interact
ensure zf-missionfollowups
ensure rhd_pizzadelivery
```
{% endcode %}
{% endstep %}
{% endstepper %}

## Dependencies

* [ox\_lib](https://github.com/overextended/ox_lib/releases)
* [ESX](https://github.com/esx-framework/esx_core/tree/main/\[core]/es_extended) or [QBCore](https://github.com/qbcore-framework/qb-core)
* [ox\_target](https://github.com/overextended/ox_target/releases) or [qb-target](https://github.com/qbcore-framework/qb-target) or [interact](https://github.com/darktrovx/interact)
* [zf-missionfollowups](https://github.com/zf-labo/zf-missionfollowups)
