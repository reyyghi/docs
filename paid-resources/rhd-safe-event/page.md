# 📄 Callback

### Create

```lua
callback.new(name, cb)
```

Example:

```etlua
callback.new('rhd_testClient', function(a1, a2)
    print(a1, a2)
    return 'Reyghita', 'Hafizh', 'Firmanda'
end)
```

* name: `string`&#x20;
* cb: `function`&#x20;

### Callback

{% tabs %}
{% tab title="Client" %}
```lua
callback.execute(name, delay, cb, args)
```

Example:

```etlua
callback.execute('rhd_testClient', 1500, function(p1, p2, p3)
    print(p1, p2, p3)
end, 'RHD', 'TEAM')
```

* name: `string`&#x20;
* delay: `number`
* cb: `function`
* args?: `any`&#x20;
{% endtab %}

{% tab title="Server" %}
```lua
callback.execute(name, source, cb, args)
```

Example:

```etlua
callback.execute('rhd_testClient', source, function(p1, p2, p3)
    print(p1, p2, p3)
end, 'RHD', 'TEAM')
```

* name: `string`&#x20;
* source: `string | integer`&#x20;
* cb: `function`
* args?: `any` &#x20;
{% endtab %}
{% endtabs %}

### Promise

{% tabs %}
{% tab title="Client" %}
```etlua
callback.execute.sync(name, delay, args)
```

Example:

```etlua
local cbExecute = callback.execute.sync
local p1, p2, p3 = cbExecute('rhd_testClient', 1500, 'RHD', 'TEAM')
print(p1, p2, p3)
```

* name: `string`&#x20;
* delay: `number`
* args?: `any`&#x20;
{% endtab %}

{% tab title="Server" %}
```etlua
callback.execute.sync(name, source, args)
```

<pre class="language-etlua"><code class="lang-etlua">local cbExecute = callback.execute.sync
<strong>local p1, p2, p3 = cbExecute('rhd_testClient', source, 'RHD', 'TEAM')
</strong>print(p1, p2, p3)
</code></pre>

* name: `string`&#x20;
* source: `playerId`
* args?: `any`&#x20;
{% endtab %}
{% endtabs %}
