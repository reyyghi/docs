---
description: >-
  All interact actions are formated as an array containing objects with the
  following properties.
icon: gear
---

# Interact Options

## InteractOptions

* name?: `string`
* label: `string`
* icon?: `string (fontawesome icon)`
* key?: `string (default: E)`
* progress?: `ProgressProps`
* distance?: `number`
* pointDistance?: `number`
* groups?: `string | string[] | table<string, number | number[]>`
* canInteract?: `function(entity, distance, coords, name, bone)`
* onSelect?: `function(data)`
* export?: `string (example: ox_inventory.openInventory)`
* event?: `string`
* serverEvent?: `string`
* command?: `string`
* args?: `any`

## ProgressProps

* duration?: `number`
* color?: `string`
* color2?: `string`
* color2Percentage?: `string`

## Callback

This is the data returned to a registered callback or event for selected option.

A selected option will trigger a single action, in order of priority:

1. onSelect
2. export
3. event
4. server event
5. command

* data: `table`
  * coords: `vector3`
  * coordsId: `string`
  * playerId: `number`
  * entity: `number`
  * distance: `number`
