<div align="center">

# sd-phone-props

**Streamed in-hand phone props for [sd-phone](https://github.com/Samuels-Development/sd-phone), in a plain and a foldable chassis, one model per frame colour.**

[**sd-phone**](https://github.com/Samuels-Development/sd-phone) · [**Documentation**](https://docs.samueldev.shop/resources/phone/) · [**Discord**](https://discord.gg/FzPehMQaBQ)

</div>

---

Streams the drawables that sd-phone attaches to the player's hand while the phone is out. The prop colour matches the phone item the player used, and the chassis matches whether the phone is a foldable:

| Set | Models | Used when |
|---|---|---|
| Plain | `sd_phone_<colour>` | `Foldable = false`, the original single-screen phone |
| Foldable, shut | `sd_phone_fold_<colour>` | `Foldable = true` and the hinge is closed |
| Foldable, open | `sd_phone_fold_<colour>_open` | `Foldable = true` and the hinge is open |

Eight colours throughout: black, blue, green, orange, pink, purple, red and yellow.

## Preview

<img width="1920" height="1280" alt="image" src="https://github.com/user-attachments/assets/f39c874c-f52d-430b-94af-41a45ada560a" />

<img width="1920" height="1280" alt="image" src="https://github.com/user-attachments/assets/6f4998d2-5c7b-4a50-9af8-5b28053d2709" />
<img width="1920" height="1280" alt="fold-open-back" src="https://github.com/user-attachments/assets/cdc54ac9-240e-413b-8351-2589fc07c376" />




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

## Foldable model

A book fold built from the same chassis, split through its thickness so the cover screen and the camera plateau end up on opposite outer faces. Shut it is 78.0 x 163.4 x 16.5 mm, the extra depth over the plain phone being the hinge: the two panels stand 3 mm apart around a recessed band, with a spine barrel down the `+X` edge so it reads as a foldable even when closed.

Open it is 156.7 x 163.4 x 9.1 mm. The two panels sit flush behind one continuous inner display and one continuous flat back, so it reads as a single device rather than two shells joined together. The grey inlay carries the full width with the SD logo centred on it, and the camera plateau stays where it is on its own half.

| Part | Shader | Texture |
|---|---|---|
| Body, hinge band, spine, plateau | `default.sps` | `sd_phone_<colour>_diffuse` 1024² BC1 |
| Cover screen (shut) | `emissive.sps` | `sd_phone_fold_cover` 512×1024 BC1 |
| Inner display (open) | `emissive.sps` | `sd_phone_fold_screen` 1024² BC1 |
| SD logo | `decal.sps` | `sd_phone_logo` 512² BC3, alpha masked |

Both screen textures are rendered from the same interface at the same wallpaper, so the cover and the left half of the inner display show an identical first home page and the phone stays consistent through a fold.

Both states keep the plain phone's origin and axes, so they weld into the same grip with no rotation of their own:

```
sd_phone_fold_<colour>        min(-0.0392, -0.0034, -0.0817)  max(0.0392, 0.0131, 0.0817)
sd_phone_fold_<colour>_open   min(-0.0784, +0.0025, -0.0817)  max(0.0784, 0.0116, 0.0817)
```

The open body is twice as wide, so sd-phone offsets it in the hand rather than leaving it centred on the grip. That offset lives in `configs/phone.lua` (`FoldOpenPropOffset`) and needs no change here.

## Credits

Phone model by **Samuels Development**.
