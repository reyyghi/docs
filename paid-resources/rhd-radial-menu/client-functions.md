# 📄 Client Functions

### AddItem

```lua
exports.rhd_radialmenu:AddItem(itemData)
```

itemData: `table`&#x20;

* id: `string`&#x20;
* title: `string`&#x20;
* icon: `string`&#x20;
* canEnable: `function`&#x20;
* action: `function(args: table | nil)` &#x20;
* event: `string`&#x20;
* serverEvent: `string`&#x20;
* command: `string`&#x20;
* export: `string` `"exports.rhd_core.getName"`&#x20;
* args: `table`&#x20;

### RemoveItem

```lua
exports.rhd_radialmenu:RemoveItem(id)
```

* id: `string`&#x20;
