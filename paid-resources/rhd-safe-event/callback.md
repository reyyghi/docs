---
icon: arrows-rotate
---

# Callback

## Create

```lua
callback.new(name, cb)
```

Example:

```lua
callback.new('rhd_testClient', function(a1, a2)
    print(a1, a2)
    return 'Reyghita', 'Hafizh', 'Firmanda'
end)
```

* name: `string`
* cb: `function`

## Callback

{% tabs %}
{% tab title="Client" %}
```lua
callback.execute(name, delay, cb, args)
```

Example:

```lua
callback.execute('rhd_testClient', 1500, function(p1, p2, p3)
    print(p1, p2, p3)
end, 'RHD', 'TEAM')
```

* name: `string`
* delay: `number`
* cb: `function`
* args?: `any`
{% endtab %}

{% tab title="Server" %}
```lua
callback.execute(name, source, cb, args)
```

Example:

```lua
callback.execute('rhd_testClient', source, function(p1, p2, p3)
    print(p1, p2, p3)
end, 'RHD', 'TEAM')
```

* name: `string`
* source: `string | integer`
* cb: `function`
* args?: `any`
{% endtab %}
{% endtabs %}

## Promise

{% tabs %}
{% tab title="Client" %}
```lua
callback.execute.sync(name, delay, args)
```

Example:

```lua
local cbExecute = callback.execute.sync
local p1, p2, p3 = cbExecute('rhd_testClient', 1500, 'RHD', 'TEAM')
print(p1, p2, p3)
```

* name: `string`
* delay: `number`
* args?: `any`
{% endtab %}

{% tab title="Server" %}
```lua
callback.execute.sync(name, source, args)
```

Example:

```lua
local cbExecute = callback.execute.sync
local p1, p2, p3 = cbExecute('rhd_testClient', source, 'RHD', 'TEAM')
print(p1, p2, p3)
```

* name: `string`
* source: `playerId`
* args?: `any`
{% endtab %}
{% endtabs %}
