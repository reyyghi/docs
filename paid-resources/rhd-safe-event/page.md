# 📄 Callback

### Create

```lua
callback.new(name, cb)
```

* name: `string`&#x20;
* cb: `function`&#x20;

### Trigger

{% tabs %}
{% tab title="Client" %}
```lua
callback.trigger(name, args)
```

* name: `string`&#x20;
* args?: `any`&#x20;
{% endtab %}

{% tab title="Server" %}
```lua
callback.trigger(name, source, args)
```

* name: `string`&#x20;
* source: `string | integer`&#x20;
* args?: `any` &#x20;
{% endtab %}
{% endtabs %}
