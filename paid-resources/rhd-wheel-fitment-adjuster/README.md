# 🛞 RHD Wheel Fitment Adjuster

### Intstallation:

{% stepper %}
{% step %}
Open the `config/server.lua` file and set access to execute commands.
{% endstep %}

{% step %}
Open the `config/mechanic.lua` file to set the mechanic location.
{% endstep %}

{% step %}
Then, start in `server.cfg` like the code below:

```lua
ensure ox_lib
ensure es_extended
ensure rhd_wfa
```
{% endstep %}
{% endstepper %}

### Dependencies:

* [ox\_lib](https://github.com/overextended/ox_lib/releases)
* [ESX](https://github.com/esx-framework/esx_core/tree/main/\[core]/es_extended) or [QBCore](https://github.com/qbcore-framework/qb-core)
