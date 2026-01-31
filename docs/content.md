# What this mod adds / changes / removes

This is a **Minecraft 1.18.2** mod that converts “go explore the infinite world” into “grow the world chunk-by-chunk”.

## Big changes

- **Overworld starts as a single chunk in the void** (a “one chunk skyworld”).
- The mod maintains a hidden **generation dimension** and **copies chunks** out of it when you expand.
- **Nether can also start empty and expand** (config option `synch_nether_chunk_spawn` defaults to true).
- Expansion is intentionally *chunk-scoped*: new chunks are “spawned” next to existing ones.

## New blocks

Names below are from the in-game language file:

- **World Core** (`chunkbychunk:worldcore`)
- **Chunk Spawner** (`chunkbychunk:chunkspawner`)
- **Themed Chunk Spawners** (restricted biome sets):
  - Forest, Plains, Desert, Jungle, Mountain, Mushroom, Swamp, Snow, Savanna, Rocky, Badlands
- **Unstable Chunk Spawner** (`chunkbychunk:unstablechunkspawner`) — spawns a random chunk
- **World Forge** (`chunkbychunk:worldforge`) — converts common blocks into “world essence” items
- **World Scanner** (`chunkbychunk:worldscanner`) — scans surrounding chunks and outputs a map heatmap
- **World Mender** (`chunkbychunk:worldmender`) — automates chunk spawning over time
- **Bedrock Chest** (`chunkbychunk:bedrockchest`) — optional special reward chest that can be “sealed”

## New items

- **World Fragment** (`chunkbychunk:worldfragment`)
- **World Shard** (`chunkbychunk:worldshard`)
- **World Crystal** (`chunkbychunk:worldcrystal`)

These are progression materials used as fuel/crafting ingredients.

## Recipes (high level)

- **World Scanner** = Compass + World Core
- **World Mender** = Dispenser + World Core
- **World Forge** = Stone crafting materials + World Core
- **Chunk Spawner** = Copper + World Core
- **Unstable Chunk Spawner** = Redstone + Copper + World Core
- **World Core** = crafted from 4 World Crystals
- **World Shard** = crafted from 4 World Fragments
- **World Crystal** = crafted from 4 World Shards

There are also “disassemble” recipes that convert back *down* the chain in some cases.

## World Forge behavior

- The World Forge consumes **fuel items** (tag-based):
  - “Soil-like” blocks (dirt/sand/gravel/etc) as weaker fuel
  - “Stone-like” blocks (cobble/deepslate cobble/etc) as stronger fuel
  - A “strong fuel” tag exists for modpacks/extension items
- It produces crystals in a stepped progression:
  - Fragment → Shard → Crystal → World Core item
- It grows the tier at a specific output count (when the output stack hits a threshold).

## World Scanner behavior

- Takes a **target** item/block and **fuel** (World Fragments/Shards/Crystals/Cores).
- Scans surrounding chunks in a spiral and writes results onto a **map** (a heatmap).
- Built-in scanner targets include ores like:
  - iron, copper, gold, redstone, lapis, diamond, emerald, coal
- It can also scan fluids (via buckets), and special-cases slime chunks.

## World Mender behavior

- Accepts either:
  - A **World Core** (treated like a basic Chunk Spawner), or
  - A **Chunk Spawner block item** (including themed or unstable spawners)
- Periodically finds a nearby missing chunk and spawns it, consuming one input per spawned chunk.

## Config options that materially change gameplay

- `enabled`: enable/disable Chunk By Chunk generation.
- `seal_world`: when true, empty chunks generate as **bedrock** (instead of being empty/void).
- `spawn_new_chunk_chest`: spawn a reward chest in newly spawned chunks.
- `use_bedrock_chest`: use the special **Bedrock Chest** reward.
- `bedrock_chest_unlock_at_blocks_remaining`: how “cleared” a chunk must be before the bedrock chest opens.
- `block_placement_allowed_outside_spawned_chunks`: whether players can place blocks into not-yet-spawned chunks.
- `start_restriction`: restrict starting location to a **Village**, a **Biome**, or **None**.

## Commands (operators)

There are server commands gated behind permission level 2:

- `chunkbychunk:spawnChunk <location>`
- `chunkbychunk:spawnRandomChunk <location>`
- `chunkbychunk:spawnThemedChunk <theme> <location>`

These only work in dimensions using the Chunk By Chunk sky-chunk generator and will refuse to overwrite non-empty chunks.

## What it “removes”

It doesn’t remove vanilla items, but it *functionally removes* the normal early-game loop of “walk 500 blocks to find biome X” by:

- Starting you in a mostly empty world.
- Requiring chunk spawning to access terrain/resources beyond your initial chunk.
