---
description: >-
  All interact actions are formated as an array containing objects with the
  following properties.
icon: gear
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: false
  outline:
    visible: false
  pagination:
    visible: true
  metadata:
    visible: false
---

# Interact Options

### InteractOptions:

***

* name?: `string`&#x20;
* label: `string`&#x20;
* icon?: `string (fontawesome icon)`&#x20;
* key?: `string (default: E)`&#x20;
* progress?: `ProgressProps`&#x20;
* distance?: `number`&#x20;
* pointDistance?: `number`&#x20;
* groups?: `string | string[] | table<string, number | number[]>`&#x20;
* canInteract?: `function(entity, distance, coords, name, bone)`&#x20;
* onSelect?: `function(data)`&#x20;
* export?: `string (example: ox_inventory.openInventory)`&#x20;
* event?: `string`&#x20;
* serverEvent?: `string`&#x20;
* command?: `string`&#x20;
* args?: `any`&#x20;

### ProgressProps:

***

* duration?: `number`&#x20;
* color?: `string`&#x20;
* color2?: `string`&#x20;
* color2Percentage?: `string`&#x20;

### Callback

***

This is the data returned to a registered callback or event for selected option.

A selected option will trigger a single action, in order of priority:

1. onSelect
2. export
3. event
4. server event
5. command

* data: `table`&#x20;
  * coords: `vector3`&#x20;
  * coordsId: `string`&#x20;
  * playerId: `number`&#x20;
  * entity: `number`&#x20;
  * distance: `number` \
