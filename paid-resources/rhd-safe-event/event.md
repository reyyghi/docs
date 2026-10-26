---
icon: bolt
---

# Event

## RegisterNetEvent

```lua
event.new(name, cb)
```

* name: `string`
* cb: `function`

## TriggerEvent

```lua
event.trigger(name, args)
```

* name: `string`
* args?: `any`

## TriggerClientEvent

```lua
event.triggerClient(name, source, args)
```

* name: `string`
* source: `number` | `number[]`
* args?: `any`

## TriggerServerEvent

```lua
event.triggerServer(name, args)
```

* name: `string`
* args?: `any`
