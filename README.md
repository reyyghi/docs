---
description: >-
  This is a trigger switching function, used to prevent cheaters from being able
  to execute events from the cheat executor.
---

# 🛡️ RHD Safe Event

{% hint style="warning" %}
Attention! If you use this, this module will automatically replace all the default trigger functions with trigger functions from the module
{% endhint %}

### Usage:

* Add a module in fxmanifest resources that wants to use the function from rhd\_safeEvent, example like the code below:

```lua
fx_version "cerulean"
game "gta5"

shared_scripts {
    '@rhd_safeEvent/trigger.lua',
    '@ox_lib/init.lua',
    'shared/main'
}

--- This is an optional, the event name written here will not be obfuscated.
safe_event_obfus_ignore {
    'vehiclekeys:client:SetOwner',
    'QBCore:Client:OnPlayerLoaded'
}

client_script "cl_main.lua"
server_script 'sv_main.lua'

lua54 "yes"
```
