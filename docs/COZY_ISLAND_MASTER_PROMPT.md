# Cozy Island — Master Design & Build Prompt

> Use this prompt as the brief for building (or overhauling into) a complete, polished cozy
> island-decorating game. It is written to be handed to a developer or a coding agent. It sets
> out the vision, the systems, the content and the acceptance criteria.

---

## 0. The one-paragraph pitch

**Cozy Island** is a relaxing, low-pressure 3D builder. You start with a tiny floating island
and a handful of objects, and you decorate it into a themed little world: a lantern-lit
Japanese garden, a candy-colored bakery cove, a spooky pumpkin patch, a beach bungalow resort.
Every object you place makes the island feel more alive. Critters move in, villagers visit,
and the island levels up. That earns new islands, new themed object packs and new tools.
Nothing can be lost, nothing is timed, and you can't fail. Progress feels like collecting
and expressing yourself, never like a chore.

---

## 1. Design pillars (every feature must serve at least one)

1. **Cozy first.** No fail states, no timers that punish, no harsh sounds. Soft palette, gentle
   motion, warm feedback.
2. **Placement feels amazing.** Snapping, previews, rotation, squash-and-stretch pop-in,
   sparkle puffs and satisfying "plink" sounds. Placing an object is the core verb, so it
   should feel like the best part of the game.
3. **Themes create meaning.** Objects belong to themed sets. Placing matching objects near
   each other forms a cohesive scene, and the game notices and rewards it.
4. **Always something to look forward to.** At any moment the player can see the next unlock,
   the next visitor, the next island and the next set to complete.
5. **The island is alive.** Day/night, weather, idle animations, wandering critters, chimney
   smoke, swaying trees, lapping water.
6. **Respect the player's time.** Sessions of 2 to 60 minutes all feel good. Autosave
   everything. Undo everything.

---

## 2. Core gameplay loop

```
 ┌─► Decorate (place / move / rotate / paint terrain)
 │        │
 │        ▼
 │   Island reacts (Charm score ↑, theme detected, critters/visitors appear)
 │        │
 │        ▼
 │   Earn rewards (Shells currency, Island XP, set progress, visitor requests completed)
 │        │
 │        ▼
 │   Unlock (new objects, themed packs, tools, colors, islands, island expansions)
 │        │
 └────────┘
```

**Micro loop (seconds):** pick object → ghost preview → place → pop animation + sound +
"+5 charm" floater.

**Mid loop (minutes):** fulfil a visitor's request ("I'd love a bench near some flowers!"),
complete a themed set, reach the next island level.

**Macro loop (days/weeks):** unlock and fully theme every island in the archipelago, complete
the Collection Book, take part in seasonal events.

---

## 3. The world: islands & archipelago

### 3.1 Island structure
- Islands are **tile grids** (start 8×8, expandable to 12×12, 16×16, 20×20) on a floating
  rocky base with a soft underside, hanging roots and small waterfalls off the edges.
- Each tile has a **terrain type**: grass, sand, dirt path, stone path, water (pond), snow,
  flowers-meadow, wooden deck, cobblestone, candy-floss (theme-specific).
- **Height levels** (0 to 3): raise and lower tiles to make hills, cliffs and terraces, with
  auto-generated slopes or steps between levels.
- Surrounding ocean with gentle shader waves, foam at the island edge, and the occasional
  jumping fish.

### 3.2 Archipelago (unlockable islands, each with a home theme and bonus)
| # | Island            | Unlock              | Home theme      | Base terrain    | Ambient          |
|---|-------------------|---------------------|-----------------|-----------------|------------------|
| 1 | Sprout Isle       | Start               | Cottage Garden  | Grass           | Birds, breeze    |
| 2 | Sunny Cove        | Island Lv 3         | Beach Resort    | Sand            | Waves, gulls     |
| 3 | Blossom Rock      | Island Lv 6         | Zen / Sakura    | Moss & stone    | Wind chimes      |
| 4 | Pinecone Peak     | Island Lv 9         | Forest Cabin    | Grass + snow    | Crackling fire   |
| 5 | Sugarplum Key     | Island Lv 12        | Candy & Bakery  | Pastel candy    | Music box        |
| 6 | Hollow Hill       | Island Lv 15        | Spooky Harvest  | Dark grass      | Owls, crickets   |
| 7 | Coral Lagoon      | Island Lv 18        | Mermaid Reef    | Shallow water   | Bubbles          |
| 8 | Starfall Isle     | Island Lv 22        | Celestial/Night | Twilight grass  | Soft synth pads  |
| 9 | Frostberry Isle   | Seasonal / Lv 25    | Winter Village  | Snow            | Sleigh bells     |

- Any object can be placed on any island. The home theme gives a **×1.5 charm bonus** for
  matching objects, which steers players without restricting them.
- An **archipelago map** view shows all islands floating together. Tap one to fly the camera
  there.

---

## 4. Placement & building system (must be excellent)

### 4.1 Core interactions
- **Ghost preview**: a translucent object follows the cursor and snaps to the tile grid. It is
  tinted green when the spot is valid and red/shaking when it isn't.
- **Rotate**: R / Q-E / two-finger twist, in 90° steps (hold Shift for 15° free rotation).
- **Footprints**: objects occupy 1×1, 1×2, 2×2 or 3×3 tiles. Show the footprint outline on
  the grid.
- **Stacking & surfaces**: some objects are **surfaces** (tables, shelves, counters, docks)
  that accept **small items** (cups, lamps, potted plants, cakes) on top. Rugs go under
  furniture.
- **Wall/edge items**: fences and hedges auto-connect to neighbors (auto-tiling: straight,
  corner, T-junction, end cap).
- **Paths** auto-blend at tile edges.
- **Move mode**: click a placed object to pick it up. It keeps its rotation and colour.
- **Multi-select & group move** (drag box or Shift-click).
- **Eyedropper**: middle-click or a long press to grab "another one of these".
- **Delete**: refunds 100% of the cost. Nothing is ever lost.
- **Undo / redo**: at least 50 steps, Ctrl+Z / Ctrl+Y, plus on-screen buttons.
- **Colour variants**: most objects have 3 to 6 palette variants, chosen with a swatch picker.
- **Free-placement toggle** for advanced players (off-grid, with collision checks).

### 4.2 Terrain tools
- Paint terrain brush (1×1, 3×3), raise/lower brush, flatten tool, water pond tool, path tool.
- Terrain changes are cheap or free, so they're tools for expression rather than a grind.

### 4.3 Feel / juice checklist
- Spawn: scale 0 → 1.15 → 1.0 over 250ms with an elastic ease, a dust/sparkle burst, and a
  pitch-randomised "plink".
- Delete: shrink and a poof of leaves or sparkles.
- Hover: a subtle bob and outline.
- Invalid: a gentle wobble and a soft "bonk", never a harsh buzzer.
- Charm gain: a floating "+N ♥" text that drifts up and fades.
- Combo: placing several matching-theme items within a few seconds gives a growing pitch
  sequence and a "Theme combo ×3!" toast.

---

## 5. Content: the object catalog (target 150+ objects at launch)

All models are **stylised low-poly**, built procedurally from primitives (or as lightweight
glTF). They use a shared pastel palette with chunky, rounded proportions and soft shading.
Each entry has: `id, name, theme, category, footprint, cost, charm, unlockLevel, tags[],
variants[], isSurface, isSmall, animated?`.

### 5.1 Categories (the catalog tabs)
Nature · Flowers · Structures · Furniture · Decor · Lights · Paths & Fences · Water ·
Critter Homes · Small Items · Special

### 5.2 Themed sets

**🌱 Cottage Garden (Starter)**
Oak tree, apple tree, round bush, flower bed (tulips, daisies, roses), picket fence,
garden gate, wooden bench, birdbath, watering can, wheelbarrow, scarecrow, vegetable patch
(carrots, cabbages), beehive, cottage house, mailbox, stone well, clothesline, garden gnome,
potted geraniums, trellis arch with vines.

**🏖️ Beach Resort**
Palm tree, coconut palm, beach umbrella, sun lounger, beach towel, sandcastle, tiki hut,
tiki torch, surfboard rack, lifeguard tower, hammock between palms, beach ball, seashell
cluster, starfish, driftwood, wooden pier/dock (surface), rowboat, ice-cream cart, lemonade
stand, bungalow, rope fence, message in a bottle.

**🌸 Zen / Sakura**
Cherry blossom tree (with falling-petal particles), bonsai, bamboo cluster, stone lantern
(tōrō), torii gate, koi pond, arched red bridge, raked sand garden, mossy boulders, stepping
stones, tea house, paper lanterns string, bamboo fence, water fountain (shishi-odoshi),
meditation cushion, pagoda, wind chime, maple tree (red).

**🌲 Forest Cabin**
Pine tree, snowy pine, log cabin, campfire (animated flames + smoke), tent, log pile,
tree stump seat, mushroom ring, fallen log, wooden signpost, canoe, lantern post, picnic
table (surface), deer statue, birdhouse, outhouse, firewood axe stump, berry bush,
fern cluster, wooden swing.

**🧁 Candy & Bakery**
Lollipop tree, gumdrop bush, candy-cane lamp post, cupcake house, gingerbread cottage,
donut swing, ice-cream cone tower, chocolate fountain, macaron stack, bakery stall
(surface), cake on stand (small), cookie-jar, sprinkle path terrain, cotton-candy cloud tree,
waffle bench, jelly pond.

**🎃 Spooky Harvest (cute, not scary)**
Pumpkin (small/large/carved with glow), haystack, crooked tree, friendly ghost (floating
anim), witch's cauldron (bubbling), wooden barn, corn stalks, scarecrow (spooky variant),
lantern-on-a-stick, picket gravestone ("RIP Boredom"), black cat statue, candle cluster,
apple-bobbing barrel, harvest wagon, owl on post, mushroom house.

**🐚 Mermaid Reef**
Coral clusters (3 types), giant clam with pearl, seaweed, sunken treasure chest, anchor,
shipwreck piece, lighthouse, sea-glass lamps, jellyfish lantern (float anim), shell throne,
bubble fountain, sand dollar path, sea turtle statue, buoy.

**✨ Celestial**
Moon lamp, star lantern, crystal cluster (glowing), telescope, observatory dome, comet
sculpture, cloud bench, astral portal ring, glowing mushrooms, constellation arch, moonflower
bed, planet orb on pedestal.

**❄️ Winter Village (seasonal)**
Snowman, igloo, festive tree (with lights), present pile, ice skating pond, sled,
gingerbread stall, frosted pine, snow globe statue, hot-cocoa stand, string lights,
reindeer statue.

**🏡 Universal / Utility (fits every theme)**
Stone path, wooden path, cobble path, hedge (auto-connect), lamp post, wooden fence,
rock (s/m/l), bench, flower pot, crates, barrels, rug, table, chair, lantern, sign, well,
fountain, bridge.

**🐾 Critter Homes (attract visitors)**
Birdhouse, bunny burrow, frog lily-pad, hedgehog leaf pile, cat bed, duck pond house,
butterfly garden, owl box, squirrel tree-hollow.

---

## 6. Progression systems (the "reasons to play")

### 6.1 Charm (the island's score)
- Each object has a base **Charm** value.
- **Theme Harmony**: every object gets a harmony multiplier based on how many same-theme
  objects are within a 2-tile radius (1.0 / 1.2 / 1.5 / 2.0). Different themes can coexist,
  but tight clusters score best.
- **Variety bonus**: unique object types on an island add bonus charm, so spamming one item
  doesn't pay.
- **Diminishing returns** per duplicate (100%, 90%, 80%… floor 40%).
- **Island Theme detection**: when 60% or more of an island's charm comes from one theme,
  the island earns that **Theme Title** (e.g. "🌸 Tranquil Garden") and a permanent bonus.
- Charm is shown as a heart meter with a 1 to 5 star **Island Rating**.

### 6.2 Island XP & levels
- Placing new objects, completing requests and finishing sets all give XP.
- Each level unlocks something concrete. Never a level with "nothing", and the next reward
  is always visible:
  - Lv 2: Paint tool · Lv 3: Sunny Cove + Beach pack · Lv 4: Colour variants · Lv 5:
    Island expansion 12×12 · Lv 6: Blossom Rock … etc.
- A level-up moment gets a fanfare, confetti, and a reward card reveal.

### 6.3 Currency: Shells 🐚
- Earned passively: each island generates shells/min based on Charm (shown in the HUD).
  Offline earnings are capped at 8 hours with a "Welcome back! You collected 240 🐚" popup.
- Earned actively: visitor requests, set completion, daily gift, achievements, and clicking
  occasional "sparkle spots" on the island.
- Spent on: objects (each placement has a cost), island expansions, new colour palettes.
- There is **no premium currency**.

### 6.4 Visitors & critters
- **Critters** (bunnies, ducks, cats, frogs, butterflies, birds, hedgehogs, owls) appear when
  their conditions are met (e.g. bunny: 3+ flowers and a bunny burrow). They wander, idle
  and react to objects (a cat sleeps on a rug, ducks swim in the pond).
- **Villagers / guests** are cute animal characters (one per theme, e.g. Pip the
  Penguin, Mochi the Bunny, Captain Gill). A guest arrives on a small boat with a
  **request**:
  - "Place 3 lanterns near the pond"
  - "Build me a cozy reading nook (bench + lamp + bookshelf)"
  - "Make this island 50% Beach theme"
  - Reward: shells, XP, and sometimes an **exclusive object** only obtainable from that
    guest.
- Guests have **friendship hearts**. At max friendship they move in permanently and give
  daily gifts.

### 6.5 Collection Book
- One page per theme showing silhouettes of undiscovered objects. Placing one reveals it.
- **Set completion** (place every object of a theme at least once) gives an exclusive
  "golden" variant of a hero object, a title, and a big shell payout.
- A page for critters met and guests befriended.

### 6.6 Quests & goals
- **Island Goals** (3 at a time, persistent, tutorial-ish): "Place your first tree",
  "Reach 100 charm", "Raise a hill".
- **Daily Cozy Tasks** (3 per day, optional, small rewards, never FOMO-punishing; missed
  days don't reset anything).
- **Achievements**, e.g. "Green Thumb: place 50 plants" or "Night Owl: play at night 10
  times".

### 6.7 Seasonal events (calendar-driven, local clock)
- Spring Bloom, Summer Festival, Harvest Moon, Winter Lights. Each gives temporary visual
  changes (snow on everything, falling leaves), an event object pack, and an event guest.
  Event items are available again in later years, so nothing is permanently missable.

### 6.8 Daily login gift
- A small wrapped present on the dock each day. Day-7 gifts are bigger. A broken streak
  never resets accumulated rewards.

---

## 7. Living world & atmosphere

- **Day/night cycle** (real-time or accelerated, toggleable). Lights and lanterns switch on at
  dusk with a warm glow and fireflies. Windows glow at night.
- **Weather**: sunny, light rain (puddle sheen, umbrella-carrying critters), snow (seasonal),
  cherry-petal wind (Blossom Rock), fog (Hollow Hill). Purely cosmetic and cozy.
- **Idle animations**: tree sway (vertex shader or bob), flag flutter, windmill spin, smoke
  particles, water ripples, bobbing boats, glowing crystals pulsing.
- **Ambient soundscape** per island plus a lofi/acoustic music playlist. Separate volume
  sliders for music, ambience and SFX.
- **Clouds** drift beneath and around the floating island.

---

## 8. Camera & controls

- Orbit (right-drag / one-finger drag on empty space), pan (middle-drag / two-finger drag),
  zoom (wheel / pinch) with smooth damping and clamped limits.
- Snap-rotate camera in 45° steps with keyboard (Q/E when not placing, or [ and ]).
- **Photo Mode**: hides the UI and adds depth of field, filters (warm, film, pastel, night),
  frames and stickers, and lets the player save a PNG.
- Full **touch support** (mobile-first-friendly), plus keyboard shortcuts with a help overlay.

---

## 9. UI / UX

- **HUD**: top-left island name + level bar; top-right shells and charm hearts; bottom a
  **catalog drawer** with category tabs, a theme filter, search, and locked items shown with
  their unlock requirement ("Unlocks at Lv 7").
- **Hotbar** of recently used items (1 to 9 keys).
- **Tooltips** on hover: name, theme icon, charm, cost, footprint.
- **Toasts** for unlocks, combos and visitor arrivals (non-blocking, stack gently).
- **Guest panel** with active requests and progress bars.
- **Settings**: audio, graphics quality (shadows, particles, pixel ratio), day/night speed,
  reduce motion, colour-blind friendly valid/invalid indicators, reset save (with confirm).
- **Onboarding**: a gentle guided first five minutes delivered by a guide character (place a
  tree, place a flower, rotate, delete/undo, meet first visitor). It can be skipped.
- Style: rounded panels, soft shadows, a rounded friendly font (e.g. "Nunito"/"Baloo"),
  pastel palette, and tactile button press animations.

---

## 10. Save system

- Autosave to `localStorage` (or IndexedDB) after every change, debounced.
- Versioned schema with migrations (`saveVersion`), so old saves never break.
- Export / import save as a JSON file or share code. Optional multiple save slots.
- Saved data: islands (tiles, heights, objects with id/pos/rot/variant), currency, XP/level,
  unlocks, collection, guests/friendship, quests, settings, last-played timestamp.

---

## 11. Technical requirements

- **Engine**: Three.js (WebGL) in a browser. A single HTML file is acceptable for a prototype,
  but the target architecture is modular (ES modules), e.g.:
  `core/ (renderer, loop, input, camera)`, `world/ (island, terrain, water, sky)`,
  `objects/ (catalog data, model factories, instancing)`, `systems/ (placement, charm,
  progression, visitors, quests, save, audio)`, `ui/`.
- **Data-driven catalog**: every object defined in a data table. Model factories are keyed by
  id, so adding an object means one data row and one builder function.
- **Performance**: 60 fps with 500+ objects on mid-range laptops/phones. Use shared
  geometries/materials, `InstancedMesh` for repeated props (flowers, grass tufts, rocks),
  frustum culling, capped pixel ratio, and optional shadows.
- **Rendering**: soft directional light + hemisphere light, PCF soft shadows, gentle fog,
  toon/flat-ish shading with subtle gradients, optional outline/postprocessing (bloom for
  lights at night).
- **Audio**: WebAudio. Synthesised SFX are fine (no external assets needed) and music can be
  procedural or loop-based.
- **No backend required.** Fully offline-capable.
- **Accessibility**: remappable keys, reduce motion, readable font sizes, never colour-only
  information.

---

## 12. Build milestones

1. **Foundation refactor**: data-driven catalog, placement state machine, undo/redo,
   save versioning.
2. **Placement polish**: ghost preview, footprints, rotation, surfaces/stacking,
   auto-connecting fences, juice.
3. **Content wave 1**: Cottage Garden + Beach + Universal (around 60 objects).
4. **Progression core**: Charm with harmony, XP/levels, shells economy, unlock gating, catalog
   locks.
5. **Living world**: day/night, critters, ambient animation, audio.
6. **Visitors & requests**, Collection Book, goals and achievements.
7. **Archipelago**: multiple islands, map view, expansions, terrain height tools.
8. **Content wave 2 & 3**: remaining themes (150+ objects).
9. **Seasonal events, photo mode, onboarding, settings, mobile polish.**

---

## 13. Acceptance criteria ("done" means)

- [ ] A new player can place, rotate, move, recolour, delete and undo within the first two
      minutes without reading anything.
- [ ] At least 150 placeable objects across 8 or more themes, each visually distinct and
      readable at default zoom.
- [ ] Every level 1 to 25 grants a visible reward, and the next reward is always on screen.
- [ ] Theme harmony visibly changes charm, and the player understands why (tooltip
      breakdown).
- [ ] At least 6 critters and at least 6 guests with requests and friendship.
- [ ] Day/night and at least 3 weather states, plus ambient audio per island.
- [ ] Saves persist across reloads, survive version updates, and can be exported and
      imported.
- [ ] Holds 60 fps with 300 objects on a mid-range laptop, and stays playable on a phone.
- [ ] Zero ways to lose progress, and zero punishing mechanics.
