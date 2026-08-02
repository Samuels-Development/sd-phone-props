<div align="center">

# sd-phone-props

**Streamed in-hand phone props for [sd-phone](https://github.com/Samuels-Development/sd-phone), one model per frame colour.**

[**sd-phone**](https://github.com/Samuels-Development/sd-phone) · [**Documentation**](https://docs.samueldev.shop/resources/phone/) · [**Discord**](https://discord.gg/FzPehMQaBQ)

</div>

---

Streams the `sd_phone_<colour>` drawables (black, blue, green, orange, pink, purple, red, yellow) that sd-phone attaches to the player's hand while the phone is out. The prop colour matches the phone item the player used.

## Installation

```cfg
ensure sd-phone-props
ensure sd-phone
```

No configuration. sd-phone resolves the prop names automatically; without this resource the phone still works, players just hold nothing visible.

## Model

Modern flat-edge chassis at real-world scale, 78.0 x 163.4 x 8.75 mm (13.5 mm over the camera plateau). 9,398 triangles, single UV channel, textures embedded in each drawable so there are no separate `.ytd` files to manage.

| Part | Shader | Texture |
|---|---|---|
| Body, plateau, buttons, charging panel | `default.sps` | `sd_phone_<colour>_diffuse` 1024² BC1 |
| Screen | `emissive.sps` | `sd_phone_screen` 512×1024 BC1 |
| SD logo | `decal.sps` | `sd_phone_logo` 512² BC3, alpha masked |

Collision is a box bound (`PLASTIC_HIGH_DENSITY`) embedded in the drawable, so the props work both attached to a ped and spawned as world objects.

## Credits

Phone model by **Samuels Development**.
