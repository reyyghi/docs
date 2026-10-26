---
description: Every client export that adds or removes interactions (model, ped, vehicle, and more).
icon: code
---

# Client Exports

| Target | Add | Remove |
| --- | --- | --- |
| [Model](model-interactions.md) | `addModel(model, options)` | `removeModel(model, name)` |
| [Ped](ped-interactions.md) | `addGlobalPed(options)` | `removeGlobalPed(optionName)` |
| [Vehicle](vehicle-interactions.md) | `addGlobalVehicle(options)` | `removeGlobalVehicle(optionName)` |
| [Object](object-interactions.md) | `addGlobalObject(options)` | `removeGlobalObject(optionName)` |
| [Player](player-interactions.md) | `addGlobalPlayer(options)` | `removeGlobalPlayer(optionName)` |
| [Local entity](local-entity-interactions.md) | `addLocalEntity(entity, options)` | `removeLocalEntity(entity, optionName)` |
| [Networked entity](networked-entity-interactions.md) | `addEntity(netId, options)` | `removeEntity(netId, optionName)` |
| [Coords](coords-interactions.md) | `addCoords(props)` | `removeCoords(coordsId, optionName)` |

Every export is called as `exports.rhd_interact:<name>(...)`. The `options` list is described in [Interact Options](../interact-options.md).
