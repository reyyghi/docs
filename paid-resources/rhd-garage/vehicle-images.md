---
description: Where vehicle images come from, how to capture your own, and where they are stored.
icon: image
---

# Vehicle Images

Each vehicle card shows the first image that loads:

1. The captured image of the model.
2. Each URL template from the **Images** tab, in order. `%s` becomes the model name.
3. A vehicle class icon.

The default URL template is `https://docs.fivem.net/vehicles/%s.webp`, which covers vanilla GTA vehicles. Add-on vehicles need a captured image or a template of your own. Templates must start with `https://` and contain `%s`.

## Capturing images

The **Images** tab of `/garageadmin` lists every registered vehicle model, add-ons included, filtered by category. Capture all of them at once, or retake or delete a single image.

{% hint style="warning" %}
Capturing needs the [screencapture](https://github.com/itschip/screencapture) resource, or `screenshot-basic`, to be running.
{% endhint %}

The capture runs on the admin's own client. Get out of your vehicle before you start.

* Each vehicle is shot twice in a studio above the ocean, on two backdrops of equal brightness. Transparency is computed from the difference between the two shots, so glass stays see-through and no paint colour is keyed out.
* The camera distance is fitted to the model dimensions. The result is cropped, given a soft ground shadow and saved as a 640x360 WebP.
* Studio position, camera angle, lights, backdrops and timings are set under `capture` in `config/main.lua`, see [Configuration](configuration.md#capture-studio).

## Storage

Choose the storage in the **Images** tab:

| Storage | Behaviour |
| --- | --- |
| **Local** (default) | Images are written to `rhd_garage/web/vehicle_images`. Players see new images after `rhd_garage` restarts, and every player downloads all images when joining |
| **Fivemanage** | Images are uploaded from the server to [Fivemanage](https://fivemanage.com). Players see them right away. A retake uploads a new file and deletes the old one |

The Fivemanage token is entered in the **Images** tab. The server checks it with Fivemanage, stores it in the server KVP, and never sends it to any client. Removing the token switches the storage back to local.

{% hint style="info" %}
With many add-on vehicles, Fivemanage keeps the join download small, because players only load the images they actually see.
{% endhint %}
