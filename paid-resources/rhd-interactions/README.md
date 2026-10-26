---
description: Interaction system for FiveM that shows options only when the player is near the right entity or coordinates.
icon: hand-pointer
---

# RHD Interactions

Add interaction options to:

* Entities (local or networked)
* Models
* Vehicles
* Objects
* Peds
* Players
* Coordinates

The interaction menu appears only when the player is near the matching entity or coordinates.

## Installation

{% stepper %}
{% step %}
Put this resource in a folder `resources/[rhd]/rhd_interact`
{% endstep %}

{% step %}
Add to `server.cfg`:

{% code title="server.cfg" %}
```cfg
ensure ox_lib
ensure rhd_interact
```
{% endcode %}
{% endstep %}

{% step %}
The resource is ready to use. See [Client Exports](client-exports/README.md) and [Interact Options](interact-options.md).
{% endstep %}
{% endstepper %}

## Dependencies

* [ox\_lib](https://github.com/overextended/ox_lib/releases)
