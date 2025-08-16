---
layout:
  width: default
  title:
    visible: false
  description:
    visible: false
  tableOfContents:
    visible: false
  outline:
    visible: false
  pagination:
    visible: true
  metadata:
    visible: false
---

# Client Functions

Properties:

```lua
---@meta

---@class ProgressBar
---@field duration number
---@field color? string
---@field color2? string
---@field color2Percentage? number

---@class DataParam
---@field entity number
---@field coords vector3
---@field distance number
---@field coordsId string
---@field playerId number

---@class OptionProps
---@field name? string
---@field label string
---@field icon? string
---@field key? string
---@field progress? ProgressBar
---@field distance? number
---@field groups? PlayerGroups
---@field canInteract? fun(entity: number, distance: number, coords: vector3, name: string, bone: string): boolean
---@field onSelect? fun(data: DataParam)
---@field export? string
---@field event? string
---@field serverEvent? string
---@field command? string
---@field args? any

---@class ModelOptions: OptionProps
---@field offset? vector3

---@class CoordsData
---@field id? string 
---@field coords vector3
---@field options OptionProps|OptionProps[]

---@class EntityOptions: OptionProps
---@field offset? vector3
---@field bones? string|string[]

---@class GlobalPedOptions: OptionProps
---@field offset? vector3

---@class GlobalObjectOptions: OptionProps
---@field offset? vector3

---@class GlobalVehicleOptions: OptionProps
---@field offset? vector3
```

#### Add Model

```lua
exports.rhd_interact:addModel(model, options)
```

* param:&#x20;
  * model: string | string\[]
  * options: ModelOptions\[]

