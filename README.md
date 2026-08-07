<div align="center">

# sd-phone-props

**Streamed in-hand phone props for [sd-phone](https://github.com/Samuels-Development/sd-phone), one model per frame colour.**

### This branch is for GTA V LEGACY

[![Enhanced build](https://img.shields.io/badge/On%20GTA%20V%20Enhanced%3F-get%20the%20enhanced%20branch-9EEADD?style=for-the-badge)](https://github.com/Samuels-Development/sd-phone-props/tree/enhanced)

[**sd-phone**](https://github.com/Samuels-Development/sd-phone) · [**Documentation**](https://docs.samueldev.shop/resources/phone/) · [**Discord**](https://discord.gg/FzPehMQaBQ)

</div>

---

Streams the `sd_phone_<colour>` drawables (black, blue, green, orange, pink, purple, red, yellow) that sd-phone attaches to the player's hand while the phone is out. The prop colour matches the phone item the player used.

## Which branch do I want

| Branch | Game build |
|---|---|
| `main` (you are here) | GTA V **Legacy** |
| [`enhanced`](https://github.com/Samuels-Development/sd-phone-props/tree/enhanced) | GTA V **Enhanced** |

The two carry the same models. Only the asset format differs: the drawables and the `.ytyp` on the `enhanced` branch have been run through CFX's Alchemist, which rewrites them into the format the Enhanced build loads. Everything else, the resource name, the manifest, the model names and the dimensions below, is identical, so sd-phone needs no change either way.

Loading the wrong branch for your build is the usual cause of an invisible or malformed prop.

## Preview

<img width="1920" height="1280" alt="image" src="https://github.com/user-attachments/assets/f39c874c-f52d-430b-94af-41a45ada560a" />

<img width="1920" height="1280" alt="image" src="https://github.com/user-attachments/assets/6f4998d2-5c7b-4a50-9af8-5b28053d2709" />

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

Local axes are X across the screen, Y through it and Z up it, origin at the geometry centre, with the screen facing `-Y`:

```
sd_phone_<colour>   min(-0.0392, -0.0068, -0.0817)  max(0.0392, 0.0068, 0.0817)
```

That is the convention GTA's own hand props use, so these weld into the `cellphone@` texting grip on `SKEL_R_Hand` (bone 28422) at a zero offset and rotation, with no per-script transform to work out.

## Credits

Phone model by **Samuels Development**.
