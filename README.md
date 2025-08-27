---
description: >-
  This is an interaction system for FiveM that allows you to add various
  interaction options, such as:
---

# 🎯 RHD Interactions

* Entities (local/netId)
* Models
* Vehicles
* Objects
* Peds
* Players
* Coordinates

With this system, you can create an interaction menu that appears only when the player is near the appropriate entity/coords.

### Installation:

{% stepper %}
{% step %}
Put this resource in a folder `resources/[rhd]/rhd_interact`&#x20;
{% endstep %}

{% step %}
Add to `server.cfg`:&#x20;

```lua
ensure ox_lib
ensure rhd_interact
```
{% endstep %}

{% step %}
Resource is ready to use.
{% endstep %}
{% endstepper %}
