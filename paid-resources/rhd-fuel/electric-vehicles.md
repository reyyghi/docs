---
description: How to set up electric vehicles in the rhd_fuel
---

# ⚡ Electric Vehicles

1. **Add model**

{% hint style="info" %}
If you're using a **gameBuild** version below 3258, you'll need to add electric vehicle models in the `config/electric.lua` file. Follow these steps:
{% endhint %}

> Open the `config/electric.lua` file and add electric vehicle models to the `vehicleModels` table. Here’s an example of how to add electric vehicle models:

```etlua
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
    "iwagen",
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

2. **Modify Values in `handling.meta`**

> Next, you'll need to modify certain values in the **`handling.meta`** file to ensure the electric vehicles function correctly.

* Change `fPetrolTankVolume`

> Search for the `fPetrolTankVolume` entry and set its value to **0.0** because electric vehicles do not use petrol tanks.

```xml
<fPetrolTankVolume value="0.0" />
```

* Change `strHandlingFlags`

> Search for the `strHandlingFlags` entry and set its value to **1000** to adjust for electric vehicles.

```xml
<strHandlingFlags value="1000" />
```

3. **Add Electric Flag in `vehicles.meta`**

> Lastly, in the **`vehicles.meta`** file, you need to add the `FLAG_IS_ELECTRIC` flag to identify the vehicle as electric. Search for the specific vehicle entry and add the flag like this:

```xml
<flags>FLAG_AVERAGE_CAR FLAG_IS_ELECTRIC FLAG_HAS_INTERIOR_EXTRAS</flags>
```
