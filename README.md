<div align="center">

# sd-phone-props

**Streamed in-hand phone props for [sd-phone](https://github.com/Samuels-Development/sd-phone): two phone designs with a choice of three logos, each plain and foldable, in 41 colours and finishes, with cases and trims to dress them.**

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

### Three logos

Every set exists with each of three marks on its back. The name starts with a different stem and is otherwise the same (`sd_ifruit_<colour>`, `sd_generic_fold_<colour>_open`, `sd_generic_dui_<colour>` and so on):

| Logo | Classic stem | Slate stem |
|---|---|---|
| SD | `sd_phone` | `sd_slate` |
| iFruit | `sd_ifruit` | `sd_ifruit_slate` |
| Plain ring, nobody's brand | `sd_generic` | `sd_generic_slate` |

### Two designs

The models above are the **classic** design: flat brushed rails, a raised camera plateau, a pill in the display. Every set also exists as **Slate**, a second design for anyone who would rather not carry that look: rounded polished rails, three lenses standing straight off the back glass, a punch-hole camera, and both buttons on one side.

| Set | Slate model |
|---|---|
| Plain | `sd_slate_<colour>` |
| Foldable, shut | `sd_slate_fold_<colour>` |
| Foldable, open | `sd_slate_fold_<colour>_open` |
| Live screen | `sd_slate_dui_<colour>`, `sd_slate_dui` |

With another logo the stem changes as in the table above (`sd_ifruit_slate_<colour>`, `sd_generic_slate_fold_<colour>`). Slate comes in the same 41 colours and is exactly the size of the classic phone with the cameras inside the same footprint, so every case and every trim position fits both. Its screens (`sd_slate_screen`, `sd_slate_fold_cover`, `sd_slate_fold_screen` in the shared dictionary) are the same pictures with the pill painted out.

With sd-phone's `Looks` setting on (`configs/phone.lua`, on by default) each player picks the design and the logo of their own phone at a case store, on its Phone tab; `Looks.Designs` says which designs the server has (both, or only one, which everybody then holds) and `Looks.Models` which logos each comes with. To make Slate the only design instead, point the classic names at it: `PropPrefix = 'sd_slate_'`, `FoldPropPrefix = 'sd_slate_fold_'`, `PropScreen.Model = 'sd_slate_dui'`.

## Preview

**[Turn every model round in the 3D viewer](https://fivem.samueldev.shop/phone/props)**: pick a logo, a body and a colour, build a case on it and see the model names it is made of.

<img width="1920" alt="The plain phone from behind and with its screen on" src="https://fivem.samueldev.shop/phone-props/readme/large_phone.jpg" />

<img width="1920" alt="The foldable shut: its back with the spine, and the cover screen" src="https://fivem.samueldev.shop/phone-props/readme/large_fold_shut.jpg" />

<img width="1920" alt="The foldable open: its back, and the inner display" src="https://fivem.samueldev.shop/phone-props/readme/large_fold_open.jpg" />

<img width="1920" alt="The iFruit logo on the plain phone and on the open foldable" src="https://fivem.samueldev.shop/phone-props/readme/large_ifruit.jpg" />

<img width="1920" alt="The Slate design: its back with three lenses straight off the glass, and its screen with a punch-hole camera" src="https://fivem.samueldev.shop/phone-props/readme/large_slate.jpg" />

<img width="1920" alt="The Slate foldable shut, open from behind, and its inner display" src="https://fivem.samueldev.shop/phone-props/readme/large_slate_fold.jpg" />

<img width="1920" alt="The SD, iFruit and plain ring logos on the classic and the Slate design" src="https://fivem.samueldev.shop/phone-props/readme/large_logos.jpg" />

<img width="1920" alt="Trims on both designs: coloured lens rings, camera surround and buttons" src="https://fivem.samueldev.shop/phone-props/readme/large_trims.jpg" />

<img width="1920" alt="The four finishes: frosted glass, polished glass, two-tone with a gold frame, leather case" src="https://fivem.samueldev.shop/phone-props/readme/large_finishes.jpg" />

<img width="1920" alt="Three phone cases close up, with patterns, accessories, stickers and charms" src="https://fivem.samueldev.shop/phone-props/readme/large_cases.jpg" />

### Everything at a glance

<img width="1920" alt="All 41 phone colours and finishes from behind" src="https://fivem.samueldev.shop/phone-props/readme/colours.jpg" />

<img width="1920" alt="The plain phone, the foldable shut and the foldable open, with the SD and the iFruit logo" src="https://fivem.samueldev.shop/phone-props/readme/bodies.jpg" />

<img width="1920" alt="Ten phone cases: shells, patterns, accessories, charms and stickers" src="https://fivem.samueldev.shop/phone-props/readme/cases.jpg" />

## Installation

```cfg
ensure sd-phone-props
ensure sd-phone
```

sd-phone resolves the prop names by itself; without this resource the phone still works, players just hold nothing visible. Each colour is one phone item, `phone_<colour>`, listed in sd-phone's `configs/phone.lua`. Ready-made 100 x 100 item icons for the SD and iFruit logos are in `extras/item_icons`.

A player who has not picked a logo holds the SD one. To make that iFruit instead (or the plain ring, with `sd_generic`), set these in sd-phone's `configs/phone.lua`:

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
| Logo, ports, grilles, screws, antenna lines | `decal.sps` | `sd_phone_details` / `sd_ifruit_details` / `sd_generic_details` 1024² BC3, shared |

The first three sets (SD on both designs, iFruit on the classic one) carry their colour atlas inside each drawable; the three added later (the plain ring on both, iFruit on Slate) take it from the dictionary, which keeps those models about a fifth smaller. Everything else lives in `stream/sd_phone_shared.ytd`, which every archetype names as its texture dictionary, so a texture is changed once for all models. The live-screen models use `stream/sd_phone_dui.ytd` instead, so sd-phone can replace `sd_phone_screen` there without touching the phones other players hold.

Each drawable carries a small cool-white light just in front of the screen, so a phone in use lights the hand and face at night. Collision is a box bound (`PLASTIC_HIGH_DENSITY`) embedded in the drawable, so the props work both attached to a ped and spawned as world objects.

Local axes are X across the screen, Y through it and Z up it, origin at the geometry centre, with the screen facing `-Y`:

```
sd_phone_<colour>             min(-0.0399, -0.0019, -0.0817)  max(0.0399, 0.0116, 0.0817)
sd_phone_fold_<colour>        min(-0.0398, -0.0035, -0.0817)  max(0.0392, 0.0103, 0.0817)
sd_phone_fold_<colour>_open   min(-0.0789, +0.0023, -0.0817)  max(0.0784, 0.0116, 0.0817)
```

That is the convention GTA's own hand props use, so these weld into the `cellphone@` texting grip on `SKEL_R_Hand` (bone 28422) at a zero offset and rotation. The open body is twice as wide, so sd-phone offsets it in the hand; that offset lives in `configs/phone.lua` (`FoldOpenPropOffset`). The plain phone's screen is 73.4 x 158.4 mm centred on `(0, -0.00186, 0)`, which is what `PropScreen.ScreenCentre` and `ScreenSize` describe.

## Trims

Small coloured parts fitted to the phone itself, with or without a case: `sd_trim_<trim>_<look>_<body>`, where the trim is `rings` (a ring round each lens), `bezel` (a band round the cameras) or `buttons` (caps over the side buttons), the look is `classic` or `slate`, and the body is `plain`, `shut` or `open`. That is 18 models. They are attached at the phone's own origin and tinted from the same 64-row palette as the cases, so a trim is any of the 64 colours, in anodised metal. A case covers the buttons; the lens rings and the camera surround show through its cut-out. Players choose them on the same Phone tab.

## Cases

sd-phone's case stores let a player design a case on their own phone in 3D and buy it as an item; using the item puts it on the phone in their hand. A case is made of separate drawables that sd-phone attaches to the phone prop, so any case goes on any phone:

| Part | Models | Tinted |
|---|---|---|
| Shell | `sd_case_<style>_<body>`: slim, gloss, fabric, leather, wallet, rugged, bumper, for `plain`, `shut` and `open` | yes |
| Pattern | `sd_case_pat_<name>_<base>`: stripes, bands, diagonal, split, slash, dots, checker, chevron, belt, waves, carbon, camo, marble, hex, topo, splatter, for `plain` and `fold` | yes |
| Accessory | `sd_case_acc_<name>`: grip, ring, loop | yes |
| Charm segment | `sd_case_charm_<segment>`: link, bead, lanyard, pearls, star, heart, moon, bolt, gem, dice, bell, coin, tag, pompom, tassel | yes, hardware stays metal |
| Icon sticker | `sd_case_stk_<name>`: star, heart, skull, flame, zap, smile, crown, ghost, rocket, music, gamepad_2, paw_print, moon, sun, cherry, gem | no |
| Brand sticker | `sd_case_stk_<brand>`: 32 of GTA's own companies, from sprunk and pisswasser to vomfeuer and zit | no |
| Photo sticker | `sd_case_stk_photo_1` to `_6`: blank cards sd-phone fills with a player's own picture | no |

Colour comes from a tint palette, not from separate models: `sd_case_pal` in `stream/sd_phone_cases.ytd` is 64 rows, one colour each, and `SetObjectTextureVariation(object, row)` picks the row for that one object. That is how 125 small models and one texture dictionary (about 5 MB together) cover every colour of every part. The shell, pattern, accessory and charm each take their own row.

| Texture | What it is |
|---|---|
| `sd_case_pal` | 256 x 64 A8R8G8B8, the palette. Row order is a contract with sd-phone (`shared/casesdata.lua`): add colours at the end only |
| `sd_case_d`, `sd_case_n` | 2048² BC1, the whitened surfaces and their normals: pebbled leather, woven fabric, knurled rubber, satin, lacquer, brushed metal. Each is drawn at 5.8 px per mm and every part is mapped onto it at that scale, so the grain is the same size on a side wall as on the back |
| `sd_case_s` | 1024² BC1, how shiny each point of those surfaces is |
| `sd_case_pat` | 4096 x 2048 BC3, the sixteen patterns as grey value x alpha |
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
