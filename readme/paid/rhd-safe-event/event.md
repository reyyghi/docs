# 📄 Event

### RegisterNetEvent

```lua
event.new(name, cb)
```

* name: `string`&#x20;
* cb: `function`&#x20;

### TriggerEvent

```lua
event.trigger(name, args)
```

* name: `string`&#x20;
* args?: `any`&#x20;

### TriggerClientEvent

```lua
event.triggerClient(name, source, args)
```

* name: `string`&#x20;
* source: `string | integer`&#x20;
* args?: `any`&#x20;

### TriggerServerEvent

```lua
event.triggerServer(name, args)
```

* name: `string`&#x20;
* args?: `any`&#x20;
