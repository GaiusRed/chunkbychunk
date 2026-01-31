# Running / Installing

## Requirements

- Minecraft **1.18.2**
- Java **17** (for building/running from source)
  - Gradle must run under Java 17 for this project.
  - If Gradle runs under Java 21, you may see: `Unsupported class file major version 65`.

### Gradle wrapper note

This repo uses Gradle via the wrapper (`gradlew`). If you see an error mentioning:

- `InclusiveRepositoryContentDescriptor.includeGroupAndSubgroups`

that typically indicates the wrapper Gradle version is too old for one of the build plugins. This repository is configured to use a newer Gradle wrapper so the build can configure successfully.
- Choose one loader:
  - **Fabric**: Fabric Loader `>=0.14.6` + **Fabric API**
  - **Forge**: Forge `40.x` (this repo uses `40.0.32`)
- Optional (nice-to-have):
  - JEI (suggested by the mod; helpful to see recipes)
  - Mod Menu (Fabric)

## Install as a player

### Fabric

1. Install Minecraft 1.18.2 + Fabric Loader.
2. Put these into your `mods/` folder:
   - Fabric API jar
   - Chunk By Chunk **Fabric** jar (typically named like `ChunkByChunk-fabric-1.18.2-<version>.jar`)
3. Launch the game.

### Forge

1. Install Minecraft 1.18.2 + Forge 40.x.
2. Put Chunk By Chunk **Forge** jar into your `mods/` folder (typically named like `ChunkByChunk-forge-1.18.2-<version>.jar`).
3. Launch the game.

## Install on a dedicated server

- Install Fabric or Forge server for Minecraft 1.18.2.
- Put the matching Chunk By Chunk jar in the server’s `mods/` folder.
- Start the server once to generate config, then adjust configs if desired.

## Create a world that uses Chunk By Chunk

On the Create World screen, look for a world type / generator option named:

- **One Chunk** (`generator.chunkbychunk.onechunkskyworld`)
- **Sealed World** (`generator.chunkbychunk.onechunksealedworld`)

If you don’t pick a Chunk By Chunk generator, the mod’s chunk-limiting gameplay may not apply.

## Running from source (dev)

This repository is based on the MultiLoader Template, with subprojects:

- `Common/`
- `Fabric/`
- `Forge/`

### Common gotcha: make sure Gradle uses Java 17

You can have Java 21 installed system-wide and still run this project — you just need **Gradle** to use **JDK 17**.

#### Installing JDK 17 via Scoop (Windows)

If you already use Scoop for Java, the most straightforward JDK 17 install is Temurin 17:

```powershell
scoop bucket add java
scoop install temurin17-jdk
```

Confirm:

```powershell
java -version
```

If you keep multiple Java versions installed with Scoop and want to switch the active one:

- Make JDK 17 the active `java`:
  - `scoop reset temurin17-jdk`
- Switch back to your Java 21 later (package name depends on what you installed, e.g. `openjdk21`):
  - `scoop reset openjdk21`

On Windows/PowerShell you have three common options:

**Option A (recommended): set `JAVA_HOME` for just this terminal**

1. Install a JDK 17 (e.g. Temurin 17).
2. In PowerShell, set it for the current session (replace the path with your actual JDK 17 path):

  ```powershell
  $env:JAVA_HOME = "C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.x.x-hotspot"
  $env:Path = "$env:JAVA_HOME\\bin;$env:Path"
  java -version
  ```

**Option B: tell Gradle which Java to use (no env var changes)**

If you know your JDK 17 path, you can run:

```powershell
./gradlew.bat -Dorg.gradle.java.home="C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.x.x-hotspot" :Fabric:runClient
```

If you installed JDK 17 via Scoop, you can also point Gradle at it like this:

```powershell
./gradlew.bat -Dorg.gradle.java.home="$(scoop prefix temurin17-jdk)" :Fabric:runClient
```

**Option C: upgrade Gradle (repo change)**

It’s possible to upgrade the Gradle wrapper so it runs on Java 21+, but that’s a project maintenance change and may require additional plugin updates. This guide assumes the simplest route: use JDK 17 for Gradle.

### Useful Gradle tasks (typical)

From the repository root:

- Build:
  - `./gradlew :Fabric:build`
  - `./gradlew :Forge:build`
- Run client:
  - `./gradlew :Fabric:runClient`
  - `./gradlew :Forge:Client`
- Run server:
  - `./gradlew :Fabric:runServer`
  - `./gradlew :Forge:Server`

Note: in this repo’s ForgeGradle setup the run tasks are named `Client`/`Server` (capitalized) rather than the more common `runClient`/`runServer`. If your environment differs, list tasks with `./gradlew tasks` (after fixing your Java version).

## Where configs live

The mod has a config system with sections like **ChunkGeneration**, **Gameplay**, **WorldForge**, **WorldScanner**, **WorldMender**, and **BedrockChest**. The exact file location depends on loader/platform, but typically ends up under something like:

- `config/` (client/server instance)

If you already use the upstream wiki, it may have more detailed packmaker-oriented configuration guidance.
