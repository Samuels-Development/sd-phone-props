<div align="center">

# sd-phone-props

**Streamed in-hand phone props for [sd-phone](https://github.com/Samuels-Development/sd-phone): a plain and a foldable chassis in 41 colours and finishes, with an SD or an iFruit logo.**

[**sd-phone**](https://github.com/Samuels-Development/sd-phone) · [**Documentation**](https://docs.samueldev.shop/resources/phone/) · [**Discord**](https://discord.gg/FzPehMQaBQ)

</div>

---

Streams the drawables that sd-phone attaches to the player's hand while the phone is out. The prop colour matches the phone item the player used, and the chassis matches whether the phone is a foldable:

| Set | Models | Used when |
|---|---|---|
| Plain | `sd_phone_<colour>` | `Foldable = false`, the single-screen phone |
| Foldable, shut | `sd_phone_fold_<colour>` | `Foldable = true` and the hinge is closed |
| Foldable, open | `sd_phone_fold_<colour>_open` | `Foldable = true` and the hinge is open |
| Live screen | `sd_phone_dui_<colour>`, `sd_phone_dui` | `PropScreen.Enabled = true`: the phone UI is drawn on the prop's own screen |

Every set also exists with the iFruit logo in place of the SD one, under `sd_ifruit_` (`sd_ifruit_<colour>`, `sd_ifruit_fold_<colour>` and so on).

## Preview

**[Turn every model round in the 3D viewer](https://fivem.samueldev.shop/phone/props)**: pick a logo, a body and a colour, build a case on it and see the model names it is made of.

<img width="1920" alt="All 41 phone colours and finishes from behind" src="https://fivem.samueldev.shop/phone-props/readme/colours.jpg" />

<img width="1920" alt="The plain phone, the foldable shut and the foldable open, with the SD and the iFruit logo" src="https://fivem.samueldev.shop/phone-props/readme/bodies.jpg" />

<img width="1920" alt="Ten phone cases: shells, patterns, accessories, charms and stickers" src="https://fivem.samueldev.shop/phone-props/readme/cases.jpg" />

## Installation

```cfg
ensure sd-phone-props
ensure sd-phone
```

sd-phone resolves the prop names by itself; without this resource the phone still works, players just hold nothing visible. Each colour is one phone item, `phone_<colour>`, listed in sd-phone's `configs/phone.lua`. Ready-made 100 x 100 item icons for both logos are in `extras/item_icons`.

To hand out iFruit phones instead, set these in sd-phone's `configs/phone.lua`:

```lua
PropPrefix     = 'sd_ifruit_',
FoldPropPrefix = 'sd_ifruit_fold_',
-- and, with PropScreen on:
PropScreen = { Model = 'sd_ifruit_dui', ... },
```

## Colours and finishes

| Finish | Colours |
|---|---|
| Frosted glass | black, blue, green, orange, pink, purple, red, yellow, white, silver, graphite, titanium, gold, rosegold, bronze, mocha, cream, burgundy, coral, peach, lime, mint, sage, forest, teal, cyan, skyblue, navy, indigo, lavender, magenta, rose |
| Polished glass | jetblack, pearl, ruby, sapphire |
| Two-tone, a gold frame | blackgold, whitegold |
| Leather case | leather_brown, leather_black, leather_tan |

## Model

Flat-edge chassis at real-world scale, 78.4 x 163.4 x 8.75 mm (13.5 mm over the camera plateau), about 5,200 triangles with a 1,100 triangle distance mesh that takes over at 12 m. Brushed frame with polished chamfers and antenna lines, raised side buttons, three lens turrets with sunken glass, flash, depth sensor, USB-C port, speaker grilles, screws and SIM tray.

The foldable is a book fold that closes flat: two 4.6 mm panels with a thin gasket between them and a three-part polished spine down the `+X` edge. Its camera is a two-lens bar on the free edge. Shut it is 78.9 x 163.4 x 13.7 mm with the cover screen on the front. Open it is 157.3 x 163.4 x 9.2 mm: the folding display sits inside a raised lip on the front, and the back shows the camera panel beside the cover screen, switched off, with the hinge as a strip between them.

A leather-case colour is the same phone inside a case that wraps the sides and back, with a lip over the edge of the glass and a raised rim round the camera cut-out. On the foldable the case covers both panels and leaves the hinge bare.

| Part | Shader | Texture |
|---|---|---|
| Body, frame, buttons, lenses, case | `normal_spec.sps` | `sd_phone_<colour>_diffuse` 512² BC1, embedded; `sd_phone_normal`, `sd_phone_spec` shared |
| Screen | `emissive.sps` | `sd_phone_screen`, `sd_phone_fold_cover` 1024 x 2048, `sd_phone_fold_screen` 2048², shared |
| Logo, ports, grilles, screws, antenna lines | `decal.sps` | `sd_phone_details` / `sd_ifruit_details` 1024² BC3, shared |

Only the colour atlas is embedded in each drawable. Everything else lives in `stream/sd_phone_shared.ytd`, which every archetype names as its texture dictionary, so a texture is changed once for all models. The live-screen models use `stream/sd_phone_dui.ytd` instead, so sd-phone can replace `sd_phone_screen` there without touching the phones other players hold.

Each drawable carries a small cool-white light just in front of the screen, so a phone in use lights the hand and face at night. Collision is a box bound (`PLASTIC_HIGH_DENSITY`) embedded in the drawable, so the props work both attached to a ped and spawned as world objects.

Local axes are X across the screen, Y through it and Z up it, origin at the geometry centre, with the screen facing `-Y`:

```
sd_phone_<colour>             min(-0.0399, -0.0019, -0.0817)  max(0.0399, 0.0116, 0.0817)
sd_phone_fold_<colour>        min(-0.0398, -0.0035, -0.0817)  max(0.0392, 0.0103, 0.0817)
sd_phone_fold_<colour>_open   min(-0.0789, +0.0023, -0.0817)  max(0.0784, 0.0116, 0.0817)
```

That is the convention GTA's own hand props use, so these weld into the `cellphone@` texting grip on `SKEL_R_Hand` (bone 28422) at a zero offset and rotation. The open body is twice as wide, so sd-phone offsets it in the hand; that offset lives in `configs/phone.lua` (`FoldOpenPropOffset`). The plain phone's screen is 73.4 x 158.4 mm centred on `(0, -0.00186, 0)`, which is what `PropScreen.ScreenCentre` and `ScreenSize` describe.

## Cases

sd-phone's Cases app lets a player design a case, buy it and wear it on the phone in their hand. A case is made of separate drawables that sd-phone attaches to the phone prop, so any case goes on any phone:

| Part | Models | Tinted |
|---|---|---|
| Shell | `sd_case_<style>_<body>`: slim, gloss, fabric, leather, wallet, rugged, bumper, for `plain`, `shut` and `open` | yes |
| Pattern | `sd_case_pat_<name>_<base>`: stripes, bands, diagonal, split, slash, dots, checker, chevron, belt, waves, carbon, camo, marble, hex, topo, splatter, for `plain` and `fold` | yes |
| Accessory | `sd_case_acc_<name>`: grip, ring, loop | yes |
| Charm segment | `sd_case_charm_<segment>`: link, bead, lanyard, pearls, star, heart, moon, bolt, gem, dice, bell, coin, tag, pompom, tassel | yes, hardware stays metal |
| Icon sticker | `sd_case_stk_<name>`: star, heart, skull, flame, zap, smile, crown, ghost, rocket, music, gamepad_2, paw_print, moon, sun, cherry, gem | no |
| Brand sticker | `sd_case_stk_<brand>`: 32 of GTA's own companies, from sprunk and pisswasser to vomfeuer and zit | no |
| Photo sticker | `sd_case_stk_photo_1` to `_6`: blank cards sd-phone fills with a player's own picture | no |

Colour comes from a tint palette, not from separate models: `sd_case_pal` in `stream/sd_phone_cases.ytd` is 64 rows, one colour each, and `SetObjectTextureVariation(object, row)` picks the row for that one object. That is how 125 small models (about 1.6 MB) cover every colour of every part. The shell, pattern, accessory and charm each take their own row.

| Texture | What it is |
|---|---|
| `sd_case_pal` | 256 x 64 A8R8G8B8, the palette. Row order is a contract with sd-phone (`shared/casesdata.lua`): add colours at the end only |
| `sd_case_d`, `sd_case_n`, `sd_case_s` | 512² whitened surfaces (smooth, gloss, rubber, metal, leather, fabric), their normals and shine |
| `sd_case_pat` | 2048 x 1024 BC3, the sixteen patterns as grey value x alpha |
| `sd_case_stk` | 1024² BC3, the icon sticker sheet. Glyphs are from [Lucide](https://lucide.dev) (ISC) |
| `sd_case_brand` | 2048 x 1024 BC3, the brand stickers: each company's mark from the game's own stock-exchange site, on a badge |
| `sd_case_photo_1` to `_6` | 64² placeholders, one per photo slot. sd-phone replaces each at runtime with an off-screen page showing a picture |

A charm is a chain: sd-phone hangs its segments one under another from the phone's bottom corner (a pendant is `link` then the pendant; `beads` is six `bead` segments; the lanyard and the pearls are one piece each) and swings them every frame, so each segment's model has its origin at the top and hangs down `-Z`. Metal hardware on a charm is a second, untinted material.

Shells use `normal_spec_tnt.sps`, patterns `decal_tnt.sps`, stickers `decal.sps`. Parts are placed by sd-phone in the phone prop's own space. A pattern plate floats 0.3 mm off the shell's back and a sticker 0.5 mm, because separate objects are positioned with single-precision world coordinates and anything closer can draw in either order.

## Changing the screen

The screens show the phone's home page. `extras` holds two drop-in alternates of the shared dictionary:

| Folder | Screens show |
|---|---|
| `extras/screens_lock` | the lock screen with notifications |
| `extras/screens_off` | a dark pane, as if the phone were asleep |

Copy the `sd_phone_shared.ytd` from one of them over `stream/sd_phone_shared.ytd` and restart the resource. Players already connected keep the old texture until they reconnect.

## Credits

Phone and case models by **Samuels Development**. The iFruit mark and the brand sticker marks are Rockstar Games' own, from Grand Theft Auto V. Sticker glyphs from [Lucide](https://lucide.dev), ISC licence.
