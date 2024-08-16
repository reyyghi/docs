# 📄 Server Functions

### install

To add nitrous to a vehicle from another resource

```lua
exports.rhd_nitrous:install(source, netId, type)
```

* source: `number`&#x20;
* netId: `integer`
* type: `number` `1 | 2 | 3`&#x20;
  1. default colour
  2. blue colour
  3. red colour

### setLevel

To adjust the nitrous level on a vehicle equipped with nitrous

```lua
exports.rhd_nitrous:setLevel(source, netId, level)
```

* source: `number`
* netId: `integer`&#x20;
* level: `number`&#x20;

### getLevel

To get the nitrous level on a vehicle that has been fitted with nitrous

```lua
exports.rhd_nitrous:getLevel(netId)
```

* netId: `integer`&#x20;
