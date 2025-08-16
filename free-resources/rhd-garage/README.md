---
description: >-
  This is an ESX and QBCore compatible garage script, made with love by the RHD
  team.
hidden: true
---

# 🅿️ RHD Garage

### Installation:

1. Run SQL according to the framework you use
2. If you use QB-Phone then you have to change several codes as below

{% hint style="warning" %}
If you use QB-Phone then you have to change several codes as below
{% endhint %}

{% tabs %}
{% tab title="QB-Phone Default" %}
1. client/main.lua `line:302`&#x20;

```lua
PhoneData.GarageVehicles = exports.rhd_garage:getvehForPhone()
```

2. client/main.lua `line:860`&#x20;

```lua
RegisterNUICallback('track-vehicle', function(data, cb)
    local veh = data.veh
    local success = exports.rhd_garage:trackveh(veh.plate, veh.garage)
    if success and not veh.disableTracking then
        QBCore.Functions.Notify("Your vehicle has been marked", "success")
    else
        QBCore.Functions.Notify("This vehicle cannot be located", "error")
    end
    cb("ok")
end)
```
{% endtab %}

{% tab title="QB-Phone Renewed-Scripts" %}
1. client/garage.lua `line:21`

```lua
RegisterNUICallback('SetupGarageVehicles', function(_, cb)
    vehicles = exports.rhd_garage:getvehForPhone()
end)
```

2. client/garage.lua`line:27`&#x20;

```lua
RegisterNUICallback('gps-vehicle-garage', function(data, cb)
    local veh = data.veh
    local success = exports.rhd_garage:trackveh(veh.plate, veh.garage)
    if success and not veh.disableTracking then
        QBCore.Functions.Notify("Your vehicle has been marked", "success")
    else
        QBCore.Functions.Notify("This vehicle cannot be located", "error")
    end
    cb("ok")
end)
```
{% endtab %}
{% endtabs %}

3. Prepare the configuration in `shared/config.lua`&#x20;
4. Start the `rhd_garage` resource in `server.cfg` like the code below:

```lua
ensure ox_lib
ensure es_extended
ensure rhd_garage
```

5. Enter the game and use the `/garagelist` command to create and edit garages
