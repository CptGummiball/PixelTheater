# Changelog

All notable changes to PixelTheater (formerly Cinecraft) are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [0.4.0] — 2026-07-16 — "Cinema Furnishing"

No changes to the playback pipeline whatsoever — this release turns the working
projector into a full cinema experience.

### Added
- **Snacks**: Popcorn (edible) and Soft Drink (drinkable with drink animation).
- **Vending machines**: Popcorn Machine and Drink Dispenser. Right-click buys the
  product (3 s cooldown). Sneak + right-click (owner/ops) opens the vending GUI with a
  **ghost price slot** — drop any item in it, the **stack size is the price** (empty =
  free; the owner's item is never consumed) — plus a 9-slot revenue till. Buyers pay
  with the stack in their main hand; a full till pauses sales; breaking the machine
  drops the revenue. Products are supplied endlessly (roleplay abstraction).
- **Ticket Gate**: right-click with a Cinema Ticket consumes it and emits a 20-tick
  redstone pulse (the gate is a redstone source). Sneak + right-click (owner/ops, empty
  hand) opens its GUI with a **required ticket name** field — empty accepts any Cinema
  Ticket, otherwise only tickets renamed to that exact name on an anvil.
- **Redstone for the switch blocks**: Projector Switch (ON = projector on, OFF = off)
  and Dimmer Switch (ON = lights out, OFF = restore the stored brightness step) — so a
  single lever can start the film and darken the hall at once.
  The Remote Projector Controller (opens a GUI), the Ticket Gate (redstone source) and
  the vending machines (need a paying player) intentionally have no redstone input.
- **Decoration**: Red Carpet, golden Stanchion (cords between posts are a known
  limitation), four individual Movie Poster blocks (Sci-Fi, Western, Horror, Romance)
  and a glowing CINEMA Sign (toggles on/off on right-click).
- **Advancements**: Welcome to the Cinema, Cinema Owner, The Smell of Popcorn
  (German and English).
- Interaction sounds (vanilla only) on dimmer, switches, gate and vending.
- Sorted creative tab (tech → controls → admission & snacks → decoration → items).
- Crafting recipes for every item and block, including Popcorn and Soft Drink.

### Changed
- The mod is now called **PixelTheater** (author: CptGummiball). The technical mod id
  stays `cinecraft` so existing worlds and configs keep working.
- The projection screen no longer draws over blocks standing between the player and
  the canvas (depth test was not guaranteed to be enabled).
- The vending GUI was widened so all labels fit (200 px, two-line price hint).
- Custom block models (stanchion, posters, sign) received proper parents and UVs —
  the stanchion previously rendered without a texture.

### Removed (deferred)
- The Cinema Curtain and Curtain Switch were pulled from this release at the last
  minute and may return in a later version.

## [0.3.0] — 2026-07-16

### Added
- **Cinema Ticket** — a pure roleplay/decoration item with no technical function,
  intended as an admission ticket for cinemas and events on roleplay servers.
  Crafted from paper + gold nugget.
- **Per-projector sound range** (4–128 blocks, default 32) configurable in the projector
  GUI with −/+ buttons, value and limits always visible, including a *Reset to Default*
  button. Stored per block, validated server-side, synced to all viewers, survives
  restarts and chunk reloads. Full volume within a quarter of the range, silence beyond it.
- **Remote Projector Controller** — a new control block that opens the full projector GUI
  from anywhere in the same dimension. Linked with the Cinema Tool exactly like the
  projector switch (sneak + right-click projector, then right-click the controller;
  an existing link is replaced). Sneak + right-click shows a short status line. The block
  visually indicates whether a projector is linked. The controller stores only the target
  position — the projector remains the single source of truth; edits made remotely are
  validated server-side (controller existence, link, dimension, permissions) and are
  rejected for arbitrary spoofed positions. Unloaded projector chunks are never
  force-loaded; the GUI simply refuses to open with a clear message.
- Server config `defaultSoundRange` (applies to newly placed projectors only).

### Changed
- The global client audio settings `audioFullRadius`/`audioMaxRadius` were removed in
  favor of the per-projector sound range. Old keys in `cinecraft.properties` are ignored.
  Pre-0.3.0 projectors receive the previous default (32) once and keep it as their own
  setting from then on.
- Documentation is now fully bilingual (English/German) with the updated project
  description: Cinecraft is a complete rework and major evolution of the no longer
  functional Lumière Play.

### Removed
- Russian language files. Supported languages are English and German; English is the
  fallback for missing keys.

## [0.2.0] — 2026-07-16

### Added
- **Cinema lighting system**
  - *Cinema Light* block with 16 brightness levels (0–15), changeable live without breaking the block.
  - *Dimmer Switch* block: right-click cycles the linked light group through the levels 0 → 4 → 8 → 12 → 15 → 0; sneak + right-click cycles in reverse. The current level is stored in the switch and re-applied to loaded lights after world load.
  - *Cinema Tool* item: right-click cinema lights to add/remove them from the selection, then right-click a dimmer switch to link the group (up to 64 lights per switch, same dimension). Sneak + right-click into the air clears the selection.
- **Projector Switch** block: link exactly one projector via Cinema Tool (sneak + right-click the projector, then right-click the switch). Right-click toggles playback on/off; the lit state shows whether the projector is running. Re-enabling starts playback from the beginning (live streams resume live).
- **Per-block Twitch session (optional)**: paste your Twitch `auth-token` in the projector GUI for ad-free playback of channels you are subscribed to. The token is stored only on your own computer, bound to that single block, never synced to the server or other players, removable via the Logout button, and deleted automatically when the block is broken. (A full OAuth app login cannot provide ad-free subscriber playback — Twitch's player only honors the website session token, which is why the token-paste approach is used.)
- **Server-side playback (experimental, opt-in)**: the server can run the streaming pipeline and relay the MPEG-TS stream to viewers, so clients never contact the video source directly. Disabled by default; the server admin must enable it in `config/cinecraft-server.properties`. The projector GUI gains a *Playback: Client/Server* selector when the server allows it, with automatic fallback to client-side playback on failure.
- **Configurable audio range**: `audioFullRadius` (default 8) and `audioMaxRadius` (default 32) in `config/cinecraft.properties`.
- Legal notice section in the README.
- This changelog.

### Fixed
- Replaying an ended video no longer requires pressing Stop first — Play restarts it directly.
- Pause (redstone, projector switch, GUI, distance) had no effect: the `--clock-synchro=0`
  VLC flag makes libvlc ignore `setPause()` on callback media — but removing it causes
  constant stutter and picture fragments on live streams (PCR re-sync). Final design:
  the flag stays for smooth playback, and pausing a stream freezes the picture and mutes
  the audio while the stream keeps running underneath. Resuming a live stream therefore
  lands cleanly at the live edge; for VODs, time passes during the pause (like classic TV).
  Local files pause/resume natively at the exact position.
- Levers and other blocks could not be placed against the projector — every right-click
  opened the GUI. Holding a block now places it; the GUI opens with a free hand.
- Access mode could only be changed by the exact placing player; operators (permission
  level 2+) can now always manage access, matching the documented behavior.
- Long pauses can no longer stall the download and corrupt the stream: the freeze+mute
  pause keeps the pipeline draining, and as a safety net a session whose buffer ever
  overflowed is restarted instead of resumed.

## [0.1.0] — 2026-07-16

Initial release. A working from-scratch reimplementation of the abandoned
"Lumière Play" mod (Apache-2.0) for Minecraft 1.21.1 (Fabric).

### Added
- Craftable projector block (glass panes / iron / diamond / redstone) with GUI:
  URL field, quality (Best/1080p/720p/480p/360p), screen presets (16:9, 32:18, 21:9, 4:3),
  volume, play/pause/stop, access control (All/Owner/Ops), redstone indicator.
- Playback of YouTube (VOD + live), Twitch, Vimeo, VK, Rutube, Dailymotion,
  SoundCloud and local files on an in-world screen with sound.
- Streaming pipeline `yt-dlp → ffmpeg → VLC` with progressive MPEG-TS muxing fed to VLC
  through blocking callback media — this restores **up to 1080p on YouTube**, which broke
  for all third-party players (including the original mod) after the platform anti-bot
  changes of May 2026.
- Automatic download and self-update of yt-dlp and ffmpeg (SHA-256 verified where available);
  VLC is the only manual requirement.
- Multiplayer sync (server stores state only, playback is fully client-side),
  join-in-progress auto-start, redstone edge control, retry ladder (2s/5s/15s),
  colored status screens, 96-block lazy pause, distance-based audio fade.
- Languages: English, German, Russian.

### Fixed (compared to the original Lumière Play)
- Production texture upload used a fragile reflection hack that silently broke outside
  the dev environment — replaced with an access widener.
- The projector block had no loot table and no pickaxe tag: it could not be mined
  properly and never dropped itself.
- Playing projectors did not start for players who joined later or loaded the chunk —
  a client-side ticker now auto-starts them.
- Orphaned yt-dlp/ffmpeg processes could keep downloading forever after a crash
  (observed live: three zombie Twitch downloads, 21 GB of temp files). Cinecraft kills
  process trees, cleans up on disconnect/shutdown, and its pipe-based design lets the
  OS terminate the pipeline automatically even after a hard crash.
