# 📄 Client Functions

### Open Garage

```lua
exports.rhd_garage:openMenu(garageData)
```

#### garageData: `table`

* label: `string`&#x20;
* type: `string[]`&#x20;
  * `car`&#x20;
  * `boat`&#x20;
  * `helicopter`&#x20;
  * `planes`&#x20;
  * `motorcycle`&#x20;
  * `cycles`&#x20;
* spawnpoint: `vector4[]`&#x20;
* ignoreDist: `boolean`&#x20;
* impound: `boolean`&#x20;
* shared: `boolean`&#x20;

### Save Vehicle

```lua
exports.rhd_garage:storeVehicle(garageData)
```

#### garageData: `table`&#x20;

* label: `string`&#x20;
* type: `string[]`&#x20;
