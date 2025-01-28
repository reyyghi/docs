# ⛽ RHD Fuel

### Installation:

1. Open the `config` folder and configure it to your liking.

{% tabs %}
{% tab title="consumption.lua" %}
```lua
return {
    -- Fuel consumption by vehicle class
    class = {
        [0] = 20.0, -- Compacts
        [1] = 20.0, -- Sedans
        [2] = 20.0, -- SUVs
        [3] = 20.0, -- Coupes
        [4] = 20.0, -- Muscle
        [5] = 20.0, -- Sports Classics
        [6] = 20.0, -- Sports
        [7] = 20.0, -- Super
        [8] = 20.0, -- Motorcycles
        [9] = 20.0, -- Off-road
        [10] = 20.0, -- Industrial
        [11] = 20.0, -- Utility
        [12] = 20.0, -- Vans
        [13] = 0.0, -- Cycles
        [14] = 20.0, -- Boats
        [15] = 20.0, -- Helicopters
        [16] = 20.0, -- Planes
        [17] = 20.0, -- Service
        [18] = 20.0, -- Emergency
        [19] = 20.0, -- Military
        [20] = 20.0, -- Commercial
        [21] = 0.0, -- Trains (lol)
    },

    -- Fuel consumption by vehicle model
    custom = {
        -- [`elegy`] = 25.0,  -- Example: Fuel consumption for Elegy set to 25.0
        -- [`t20`] = 30.0,  -- Example: Fuel consumption for T20 set to 30.0
    },

    -- If you want to make a particular vehicle not consume fuel/battery, such as a bicycle, enter the spawn code in this table.
    model = {
        -- [`kuruma`] = true,  -- Kuruma will not consume fuel
        -- [`bicycle`] = true, -- Bicycle will not consume fuel
    },

    --[[ 
        Explanation for this section:
        
        1. This variable will not work on vehicles that are registered in the `model` table with a value of `true` (meaning they do not consume fuel/battery).
        If a vehicle is listed in the `model` table with `true`, it will not be affected by fuel consumption or tank volume settings.
        
        2. Do not set the value of the `global` variable in the `tankVolume` table to be below 1.0, as doing so will cause the script to not work properly.
        
        3. If you want to set a custom fuel tank volume for specific vehicles, you can add them in the `custom` table inside the `tankVolume` table. 
        This way, specific vehicles will have their own custom fuel tank volume.
    ]]
    tankVolume = {
        global = 4.0,  -- Default fuel tank volume for all vehicles is 4.0
        custom = {
            -- [`kuruma`] = 5.0,  -- Fuel tank volume for Kuruma set to 5.0
            -- [`elegy`] = 6.0,   -- Fuel tank volume for Elegy set to 6.0
        }
    }
}
```
{% endtab %}

{% tab title="electric.lua" %}
{% code fullWidth="true" %}
```lua
return {
    -- Vehicle models for electric vehicles
    -- List of vehicle models that are considered electric vehicles in the system
    -- This list includes various electric vehicle models available in the game.
    -- These models can be used to apply specific behavior or features related to electric vehicles.
    ---@see https://rhd.gitbook.io/rhd-s/paid-resources/rhd-fuel/electric-vehicles
    vehicleModels = {
        "surge",       -- Electric vehicle model "Surge"
        "iwagen",      -- Electric vehicle model "Iwagen"
        "voltic",      -- Electric vehicle model "Voltic"
        "voltic2",     -- Electric vehicle model "Voltic 2"
        "raiden",      -- Electric vehicle model "Raiden"
        "cyclone",     -- Electric vehicle model "Cyclone"
        "tezeract",    -- Electric vehicle model "Tezeract"
        "neon",        -- Electric vehicle model "Neon"
        "omnisegt",    -- Electric vehicle model "Omnisegt"
        "caddy",       -- Electric vehicle model "Caddy"
        "caddy2",      -- Electric vehicle model "Caddy 2"
        "caddy3",      -- Electric vehicle model "Caddy 3"
        "airtug",      -- Electric vehicle model "Airtug"
        "rcbandito",   -- Electric vehicle model "RC Bandito"
        "imorgon",     -- Electric vehicle model "Imorgon"
        "dilettante",  -- Electric vehicle model "Dilettante"
        "khamelion",   -- Electric vehicle model "Khamelion"
    },

    -- Electric Vehicle Charging Station Coordinates
    -- This section lists the coordinates (in vector4 format) of various electric vehicle charging stations in the game world.
    -- These stations are where players can charge their electric vehicles, and the X, Y, Z, W values ​​indicate the position and direction of the charging object.
    station = {
        vec4(53.91, 2785.72, 56.88, 55.00),       -- Charging station at location (53.91, 2785.72, 56.88) with heading 55.00
        vec4(267.40, 2598.54, 43.81, 285.00),     -- Charging station at location (267.40, 2598.54, 43.81) with heading 285.00
        vec4(1053.01, 2658.08, 38.55, 180.00),    -- Charging station at location (1053.01, 2658.08, 38.55) with heading 180.00
        vec4(1205.34, 2653.61, 36.85, 225.00),    -- Charging station at location (1205.34, 2653.61, 36.85) with heading 225.00
        vec4(2675.96, 3270.41, 54.41, 150.00),    -- Charging station at location (2675.96, 3270.41, 54.41) with heading 150.00
        vec4(2003.37, 3780.78, 31.18, 120.00),    -- Charging station at location (2003.37, 3780.78, 31.18) with heading 120.00
        vec4(1695.88, 4925.88, 41.23, 325.00),    -- Charging station at location (1695.88, 4925.88, 41.23) with heading 325.00
        vec4(1704.83, 6425.96, 31.77, 65.00),     -- Charging station at location (1704.83, 6425.96, 31.77) with heading 65.00
        vec4(128.15, 6632.35, 30.86, 135.00),     -- Charging station at location (128.15, 6632.35, 30.86) with heading 135.00
        vec4(-88.27, 6415.91, 30.64, 315.00),     -- Charging station at location (-88.27, 6415.91, 30.64) with heading 315.00
        vec4(-1430.71, -266.71, 45.27, 40.00),    -- Charging station at location (-1430.71, -266.71, 45.27) with heading 40.00
        vec4(-2074.65, -323.92, 12.32, 355.00),   -- Charging station at location (-2074.65, -323.92, 12.32) with heading 355.00
        vec4(-705.29, -917.44, 18.21, 90.00),     -- Charging station at location (-705.29, -917.44, 18.21) with heading 90.00
        vec4(-531.22, -1219.62, 17.46, 245.00),   -- Charging station at location (-531.22, -1219.62, 17.46) with heading 245.00
        vec4(-53.0297, -1769.3372, 28.1935, 49.9402), -- Charging station at location (-53.0297, -1769.3372, 28.1935) with heading 49.9402
    },

    -- Blip settings for the charging stations
    -- This section defines the properties of the blip that will appear on the map for charging stations.
    -- The blip is used to show players the locations of the charging stations.
    blip = {
        color = 3,    -- Color of the blip on the map (3 is a light blue color in GTA V)
        sprite = 620, -- The sprite ID for the blip (620 corresponds to a charging station in GTA V)
        nearest = false, -- Whether to show the blip for the nearest station to the player (false means it will show all stations)
    }
}
```
{% endcode %}
{% endtab %}

{% tab title="fuel.lua" %}
```lua
return {
    useRope = true,
    pumpModel = {
        `prop_gas_pump_1d`,
        `prop_gas_pump_1a`,
        `prop_gas_pump_1b`,
        `prop_gas_pump_1c`,
        `prop_vintage_pump`,
        `prop_gas_pump_old2`,
        `prop_gas_pump_old3`,
    },
    station = {
        vector3(49.4187, 2778.793, 58.043),
        vector3(263.894, 2606.463, 44.983),
        vector3(1039.958, 2671.134, 39.550),
        vector3(1207.260, 2660.175, 37.899),
        vector3(2539.685, 2594.192, 37.944),
        vector3(2679.858, 3263.946, 55.240),
        vector3(2005.055, 3773.887, 32.403),
        vector3(1687.156, 4929.392, 42.078),
        vector3(1701.314, 6416.028, 32.763),
        vector3(179.857, 6602.839, 31.868),
        vector3(-94.4619, 6419.594, 31.489),
        vector3(-2554.996, 2334.40, 33.078),
        vector3(-1800.375, 803.661, 138.651),
        vector3(-1437.622, -276.747, 46.207),
        vector3(-2096.243, -320.286, 13.168),
        vector3(-724.619, -935.1631, 19.213),
        vector3(-526.019, -1211.003, 18.184),
        vector3(-70.2148, -1761.792, 29.534),
        vector3(265.648, -1261.309, 29.292),
        vector3(819.653, -1028.846, 26.403),
        vector3(1208.951, -1402.567,35.224),
        vector3(1181.381, -330.847, 69.316),
        vector3(620.843, 269.100, 103.089),
        vector3(2581.321, 362.039, 108.468),
        vector3(176.631, -1562.025, 29.263),
        vector3(176.631, -1562.025, 29.263),
        vector3(-319.292, -1471.715, 30.549),
        vector3(1784.324, 3330.55, 41.253),
    },
    blip = {
        color = 60,
        sprite = 361,
        nearest = false
    }
}
```
{% endtab %}

{% tab title="interface.lua" %}
```lua
return {
    -- Option for the interaction system, can use 'ox_target', 'qb-target', or 'interact'
    interact = 'qb-target',

    -- Option for the progress bar system, can use 'qb', 'ox', or 'refine'
    progressbar = 'qb'
}
```
{% endtab %}

{% tab title="main.lua" %}
```lua
return {
    price = {
        -- The price for refueling per 1 liter of fuel
        refuel = 100,

        -- The price for purchasing 1 petrol can (container)
        petrolcan = 1000,

        -- The price for refilling 1 petrol can (container)
        refilPetrolcan = 500,

        -- The price for charging, per 1% of battery charge
        charger = 100
    },

    bridge = {
        -- List of fuel systems (bridges) that the server uses for fuel management
        'ps-fuel',
        'cdn-fuel',
        'LegacyFuel',
    },

    -- Fine amount for nozzle violations (or set to false to disable fines)
    -- Represents the penalty if something goes wrong with the fuel nozzle
    nozzleFine = 1000,

    -- Whether the fuel nozzle can explode (set to true to enable explosions or false to disable)
    nozzleExplosion = true
}

```
{% endtab %}
{% endtabs %}

1. Then, start in `server.cfg` like the code below:

```lua
ensure ox_lib
ensure es_extended

ensure ox_inventory
ensure interact
ensure rhd_fuel
```

### Dependencies:

* [ox\_lib](https://github.com/overextended/ox_lib/releases)
* [ox\_inventory](https://github.com/overextended/ox_inventory/releases) or [qb-inventory](https://github.com/qbcore-framework/qb-inventory)
* [ESX](https://github.com/esx-framework/esx_core/tree/main/\[core]/es_extended) or [QBCore](https://github.com/qbcore-framework/qb-core)
* [ox\_target](https://github.com/overextended/ox_target/releases) or [qb-target](https://github.com/qbcore-framework/qb-target) or [interact](https://github.com/darktrovx/interact)
