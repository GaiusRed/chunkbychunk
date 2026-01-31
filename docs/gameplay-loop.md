# Gameplay loop (happy path — best guess)

This is an inferred “intended loop” based on advancements, recipes, and block/entity behavior.

## The core loop

1. **Start in a one-chunk skyworld**
   - You begin with **~1 chunk** available (configurable).
   - Everything beyond is “missing/empty” until you spawn it.

2. **Acquire or craft a World Core**
   - A lot of progression gates off the **World Core**:
     - Chunk Spawner
     - World Scanner
     - World Mender
     - World Forge

   How you get your first one depends on config/loot:
   - New chunks may include a reward chest containing world materials (and sometimes cores/crystals/spawners).

3. **Craft and use a Chunk Spawner to expand**

- Craft a **Chunk Spawner** (Copper + World Core).
- Place it **next to the edge** of your existing world, adjacent to an empty/missing chunk.
- Interact with it to **spawn** a new chunk copied from the generation dimension.

4. **Harvest new resources from each spawned chunk**

- Each new chunk can bring:
  - stone, ores, trees, structures, etc (whatever was in the source chunk)
- If enabled, newly spawned chunks can include a **reward chest** at depth.
  - With Bedrock Chest enabled, the chest may be “sealed” until you clear enough blocks above it.

5. **Convert common blocks into “world essence” (World Forge)**

Once you can build a **World Forge**:

- Feed it lots of common blocks (dirt/sand/gravel and cobble/deepslate cobble).
- It slowly produces:
  - World Fragment → World Shard → World Crystal → (eventually) World Core items

This becomes your “industrial” way to make more Cores without relying purely on chest RNG.

6. **Plan expansion using the World Scanner**

Once you can build a **World Scanner**:

- Insert a target item (e.g., “diamond”, “iron”, etc) and fuel it with fragments/shards/crystals/cores.
- The scanner generates a **map heatmap** of nearby chunks showing the concentration of that target.
- Use that information to choose *which direction* to spawn next chunks.

7. **Automate expansion (World Mender)**

Once you can build a **World Mender**:

- Put a stack of **Chunk Spawners** (or World Cores, which behave like basic spawners) into it.
- It will periodically spawn the nearest missing chunk within a radius, consuming inputs.

## Variations / knobs

### Themed Chunk Spawners

The mod includes spawners like **Forest Chunk Spawner**, **Desert Chunk Spawner**, etc.

Best guess for intended use:

- When you need a particular biome’s “starter kit” (trees, sand, snow, etc), use a themed spawner.
- Biome themes are defined (for Overworld) as named groups like `plains`, `snow`, `desert`, etc.

### Unstable Chunk Spawner

The **Unstable Chunk Spawner** spawns a random chunk.

Best guess for intended use:

- Quick variety / exploration substitute.
- When you don’t care where resources come from, you just need “more world”.

### Nether synchronization

If `synch_nether_chunk_spawn` is enabled:

- The Nether can start empty too.
- Overworld chunk spawns can trigger corresponding Nether chunk spawns (scaled to Nether coordinates).

## “Winning” / long-term play

There isn’t a single explicit win condition in the repo, but the loop naturally aims at:

- expanding enough to access diverse resources/biomes,
- stabilizing the world-material economy (World Forge → more World Cores),
- using the Scanner + themed spawners to deliberately target resources,
- and optionally fully automating chunk expansion with the World Mender.
