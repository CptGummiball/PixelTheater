# 🎬 PixelTheater

**[English](#-english)** · **[Deutsch](#-deutsch)**

---

## 🇬🇧 English

**Version 0.4.0 · Minecraft 1.21.1 · Fabric · by CptGummiball**

PixelTheater turns Minecraft into a cinema: place a projector, paste a YouTube, Twitch
or file link, and everyone nearby watches together on a screen in your world — complete
with cinema lighting, ticket gates, vending machines and remote controls.

> Cinecraft (now PixelTheater) is a complete rework and major evolution of the no longer
> functional Lumière Play mod (Apache-2.0) for Minecraft 1.21.1 (Fabric). While
> originally based on Lumière Play, it has since been extensively redesigned, expanded,
> and improved with a modern streaming pipeline, new cinema-management features,
> dedicated control blocks, enhanced playback options, and a more robust overall
> architecture built to remain functional after the platform anti-bot crackdowns of 2026.

*Note: the technical mod id is `cinecraft` — that was the project's working title. To
avoid breaking bugs (placed blocks and configs are tied to the id), the mod id stays
unchanged; only the display name is PixelTheater.*

### ✨ Features

- **Projector block** — right-click, paste a link, press Play
- **Platforms**: YouTube (VOD + live), Twitch, Vimeo, VK, Rutube, Dailymotion, SoundCloud, local files
- **Quality**: Best / 1080p / 720p / 480p / 360p · **Screen presets**: 16:9, 32:18, 21:9, 4:3
- **Cinema lighting**: lights with 16 brightness levels + dimmer switch groups
- **Control blocks**: Projector Switch, Remote Projector Controller
- **Cinema Tool** for linking lights, switches and controllers
- **Per-projector sound range** (4–128 blocks) in the block GUI
- **Snacks & vending**: Popcorn Machine and Drink Dispenser with item-based pricing and a revenue till
- **Ticket Gate**: consumes a Cinema Ticket → redstone pulse; optional required ticket name
- **Redstone** on projector switch and dimmer: one lever = film on + hall dark
- **Decoration**: red carpet, stanchions, four movie posters, glowing CINEMA sign
- **Multiplayer**: server stores state only, playback is client-side; access control; auto-retry
- Optional **per-block Twitch session** and **server-side playback** (opt-in relay)
- 4 advancements · Languages: **English, German**

### 📋 Requirements & installation

| What | Why | How |
|---|---|---|
| **VLC Media Player** (64-bit, 3.x) | video decoding | [videolan.org](https://www.videolan.org/vlc/) · `sudo apt install vlc` · `brew install vlc` |
| yt-dlp | stream resolution | **automatic** — downloads itself on first run |
| ffmpeg | stream muxing | **automatic** — downloads itself on first run |
| Fabric API | | required dependency |

Install: drop `pixeltheater-<version>.jar` and Fabric API into your `mods/` folder
(Fabric loader, MC 1.21.1). The server needs no VLC — playback runs on the clients.

### 🍿 Basic usage

1. Craft the projector:

   | | | |
   |:---:|:---:|:---:|
   | 🪟 Glass Pane | 🪟 Glass Pane | 🪟 Glass Pane |
   | ⛓️ Iron Ingot | 💎 Diamond | ⛓️ Iron Ingot |
   | ⛓️ Iron Ingot | 🔴 Redstone | ⛓️ Iron Ingot |

2. Place it facing a wall — the screen appears on its front face, one block above its base.
3. Right-click → paste a URL (or a local path like `/C:/videos/movie.mp4`) → **▶ Play**.
4. Set quality, screen preset, volume and sound range to taste.

### 💡 Lighting & control blocks

- **Cinema Light** — 16 brightness levels, changed live by a linked dimmer.
- **Dimmer Switch** — right-click cycles its group 0 → 4 → 8 → 12 → 15 → 0 (sneak =
  reverse); redstone ON forces lights out, OFF restores the stored level. Max. 64
  lights per switch, same dimension.
- **Projector Switch** — toggles exactly one linked projector; redstone ON = play,
  OFF = off. Re-enabling starts from the beginning (live streams resume live).
- **Remote Projector Controller** — opens the full projector GUI from anywhere in the
  same dimension (never force-loads chunks; clear message if the projector chunk is
  unloaded). Sneak + right-click shows a status line.
- **Cinema Tool** links everything: right-click lights → select, right-click dimmer →
  link group; sneak + right-click projector → select, right-click switch/controller →
  link; sneak + right-click into the air → clear selection.

### 🎫 Ticket Gate & 🍿 vending machines

- **Cinema Ticket**: roleplay item (no function of its own). At a **Ticket Gate** it
  becomes an entry pass: right-click the gate with a ticket — it is consumed and the
  gate emits a short redstone pulse (opens doors/pistons). Sneak + right-click with an
  empty hand (owner/ops) opens the gate GUI: set a required ticket name (rename tickets
  on an anvil) or leave empty to accept any ticket.
- **Popcorn Machine / Drink Dispenser**: right-click buys popcorn / a soft drink
  (3 s cooldown). Sneak + right-click (owner/ops) opens the vending GUI: drag any item
  into the **price slot** — the stack size is the price (empty = free; your item is not
  consumed). Payments collect in the 9-slot revenue till; a full till pauses sales;
  breaking the machine drops the revenue. Buyers pay with the stack in their main hand.

### 🟣 Twitch, 🖥️ server-side playback, ⚙️ configuration

- **Per-block Twitch session**: projector GUI → *Twitch: sign in...* → paste your
  `auth-token` (browser: twitch.tv → F12 → Cookies) for ad-free playback of subscribed
  channels. Stored only on your computer, bound to that block, deleted when it breaks.
  Treat the token like a password.
- **Server-side playback (experimental, opt-in)**: the server runs the pipeline and
  relays one MPEG-TS stream to all viewers. Enable via `enableServerPlayback=true` in
  `config/cinecraft-server.properties`; ~1.2 MB/s upload per viewer, 720p cap, automatic
  fallback to client playback. Twitch sessions are never forwarded.
- `config/cinecraft.properties` (client): `vlcPath`, `cookiesFromBrowser`, `extraYtDlpArgs`.
  `config/cinecraft-server.properties` (server): `enableServerPlayback`,
  `maxServerSessions`, `streamRateKBs`, `defaultSoundRange`.
  Binaries live in `<game dir>/cinecraft/bin/`.

### 🛠️ Crafting recipes

Shaped recipes are shown in crafting-grid arrangement; empty cells mean empty slots.

**PixelTheater Projector**
| | | |
|:---:|:---:|:---:|
| Glass Pane | Glass Pane | Glass Pane |
| Iron Ingot | Diamond | Iron Ingot |
| Iron Ingot | Redstone | Iron Ingot |

**Cinema Light** (×4)
| | | |
|:---:|:---:|:---:|
| Glass | Glass | Glass |
| Glass | Glowstone | Glass |
| Iron Ingot | Iron Ingot | Iron Ingot |

**Dimmer Switch**
| |
|:---:|
| Iron Ingot |
| Redstone |
| Iron Ingot |

**Projector Switch**
| |
|:---:|
| Iron Ingot |
| Lever |
| Redstone |

**Remote Projector Controller**
| |
|:---:|
| Ender Pearl |
| Iron Ingot |
| Redstone |

**Ticket Gate**
| | | |
|:---:|:---:|:---:|
| Iron Ingot | Cinema Ticket | Iron Ingot |
| Iron Ingot | Redstone | Iron Ingot |

**Popcorn Machine**
| | | |
|:---:|:---:|:---:|
| Glass | Glass | Glass |
| Iron Ingot | Wheat Seeds | Iron Ingot |
| Iron Ingot | Iron Ingot | Iron Ingot |

**Drink Dispenser**
| | | |
|:---:|:---:|:---:|
| Iron Ingot | Iron Ingot | Iron Ingot |
| Iron Ingot | Water Bucket | Iron Ingot |
| Iron Ingot | Iron Ingot | Iron Ingot |

**Stanchion** (×2)
| |
|:---:|
| Gold Nugget |
| Gold Ingot |
| Gold Ingot |

**Red Carpet** (×3)
| | |
|:---:|:---:|
| Red Wool | Red Wool |

**CINEMA Sign**
| | | |
|:---:|:---:|:---:|
| Glass Pane | Glass Pane | Glass Pane |
| Glass Pane | Glowstone Dust | Glass Pane |
| Glass Pane | Glass Pane | Glass Pane |

**Shapeless recipes**
| Result | Ingredients |
|---|---|
| Cinema Tool | Iron Ingot + Redstone + Stick |
| Cinema Ticket (×4) | Paper + Gold Nugget |
| Popcorn (×2) | 2× Wheat Seeds + Paper |
| Soft Drink | Sugar + Glass Bottle |
| Movie Poster: Sci-Fi | 2× Paper + Blue Dye |
| Movie Poster: Western | 2× Paper + Orange Dye |
| Movie Poster: Horror | 2× Paper + Black Dye |
| Movie Poster: Romance | 2× Paper + Pink Dye |

### ⚠️ Known limitations

- Pausing a **stream** freezes picture and sound while the stream continues underneath
  (live resumes at the live edge; VOD time passes during the pause). Local files
  pause/resume at the exact position.
- "Best" quality is capped at 1080p (the screen texture is 1280×720).
- Stanchions have no connecting cords yet; macOS on Apple Silicon needs Homebrew
  ffmpeg or Rosetta 2; server-side playback is experimental and bandwidth-intensive.

### ⚖️ Legal notice

Only play content you hold the necessary rights for. Owning a DVD, Blu-ray, video file
or a personal streaming subscription does **not** automatically permit showing that
content to other players on a server. Do not use pirated streams, film rips or
unauthorized IPTV, and do not circumvent DRM, paywalls, ads or geo-blocking.
Server-side fetching, caching or relaying of video content may require additional
rights. Always comply with the terms of service of the respective platform. The server
operator is responsible for the content, sources, licenses and provider terms used;
for public, commercial or larger community servers, obtaining legal advice before use
is recommended. This notice is not legal advice. (Informational only — PixelTheater
deliberately contains no technical enforcement.)

### 🆕 What's new in 0.4.0 — "Cinema Furnishing"

- Popcorn & soft drinks with vending machines (item-based pricing, revenue till)
- Ticket Gate (redeem tickets → redstone pulse, optional name binding)
- Redstone control for projector switch and dimmer
- Red carpet, stanchions, four movie posters, glowing CINEMA sign, advancements
- Renamed to PixelTheater (author CptGummiball); no changes to the playback pipeline
- See [CHANGELOG.md](CHANGELOG.md)

### 🛠️ Building & 🐛 bugs

```
./gradlew build        # jar lands in build/libs/
./gradlew runClient    # dev client
```

Report bugs via the GitHub issue templates (include `logs/latest.log` and the URL you
tried). **License:** Apache-2.0, Copyright CptGummiball — see [LICENSE](LICENSE) and
[NOTICE](NOTICE); attribution to the original Lumière Play by jrxmod is retained, and
[vlcj](https://github.com/caprica/vlcj) is bundled.

---

## 🇩🇪 Deutsch

**Version 0.4.0 · Minecraft 1.21.1 · Fabric · von CptGummiball**

PixelTheater macht aus Minecraft ein Kino: Projektor platzieren, YouTube-, Twitch- oder
Datei-Link einfügen, und alle in der Nähe schauen gemeinsam auf einer Leinwand in eurer
Welt — komplett mit Kinobeleuchtung, Ticket-Schranken, Verkaufsautomaten und
Fernsteuerung.

> Cinecraft (jetzt PixelTheater) ist ein vollständiges Rework und eine umfassende
> Weiterentwicklung der nicht mehr funktionsfähigen Mod Lumière Play (Apache-2.0) für
> Minecraft 1.21.1 mit Fabric. Obwohl Lumière Play ursprünglich als Grundlage diente,
> wurde die Mod inzwischen umfangreich überarbeitet, erweitert und verbessert. Dazu
> gehören eine moderne Streaming-Pipeline, neue Funktionen zur Kinosteuerung, dedizierte
> Schalter und Steuerblöcke, erweiterte Wiedergabeoptionen sowie eine robustere
> Gesamtarchitektur, die auch nach den Anti-Bot-Verschärfungen der Plattformen im Jahr
> 2026 weiterhin funktionieren soll.

*Hinweis: Die technische Mod-ID lautet `cinecraft` — das war der Arbeitstitel des
Projekts. Zur Vermeidung von Breaking-Bugs (platzierte Blöcke und Configs hängen an der
ID) bleibt die Mod-ID unverändert; nur der Anzeigename ist PixelTheater.*

### ✨ Funktionen

- **Projektor-Block** — Rechtsklick, Link einfügen, Abspielen
- **Plattformen**: YouTube (Videos + Live), Twitch, Vimeo, VK, Rutube, Dailymotion, SoundCloud, lokale Dateien
- **Qualität**: Best / 1080p / 720p / 480p / 360p · **Leinwand-Presets**: 16:9, 32:18, 21:9, 4:3
- **Kinobeleuchtung**: Leuchten mit 16 Helligkeitsstufen + Dimmer-Gruppen
- **Steuerblöcke**: Projektor-Schalter, Remote-Projektorsteuerung
- **Kino-Werkzeug** zum Verknüpfen von Leuchten, Schaltern und Steuerungen
- **Sound-Reichweite pro Projektor** (4–128 Blöcke) in der Block-GUI
- **Snacks & Verkauf**: Popcorn-Maschine und Getränkeautomat mit Item-basierten Preisen und Einnahmenlager
- **Ticket-Schranke**: entwertet Kinotickets → Redstone-Puls; optionale Namensbindung
- **Redstone** an Projektor-Schalter und Dimmer: ein Hebel = Film an + Saal dunkel
- **Dekoration**: roter Teppich, Absperrpfosten, vier Filmposter, leuchtendes CINEMA-Schild
- **Multiplayer**: Server speichert nur Zustand, Wiedergabe clientseitig; Zugriffsrechte; Auto-Retry
- Optionale **Twitch-Session pro Block** und **Server-Side Playback** (Opt-in-Relay)
- 4 Fortschritte · Sprachen: **Deutsch, Englisch**

### 📋 Voraussetzungen & Installation

| Was | Wozu | Wie |
|---|---|---|
| **VLC Media Player** (64-bit, 3.x) | Video-Dekodierung | [videolan.org](https://www.videolan.org/vlc/) · `sudo apt install vlc` · `brew install vlc` |
| yt-dlp | Stream-Auflösung | **automatisch** — lädt sich beim ersten Start selbst |
| ffmpeg | Stream-Muxing | **automatisch** — lädt sich beim ersten Start selbst |
| Fabric API | | erforderliche Abhängigkeit |

Installation: `pixeltheater-<version>.jar` und Fabric API in den `mods/`-Ordner (Fabric
Loader, MC 1.21.1). Der Server braucht kein VLC — die Wiedergabe läuft auf den Clients.

### 🍿 Grundlegende Bedienung

1. Projektor craften:

   | | | |
   |:---:|:---:|:---:|
   | 🪟 Glasscheibe | 🪟 Glasscheibe | 🪟 Glasscheibe |
   | ⛓️ Eisenbarren | 💎 Diamant | ⛓️ Eisenbarren |
   | ⛓️ Eisenbarren | 🔴 Redstone | ⛓️ Eisenbarren |

2. Mit Blick zur Wand platzieren — die Leinwand erscheint an der Vorderseite, einen Block über der Basis.
3. Rechtsklick → URL einfügen (oder lokaler Pfad wie `/C:/videos/film.mp4`) → **▶ Abspielen**.
4. Qualität, Leinwand-Preset, Lautstärke und Sound-Reichweite einstellen.

### 💡 Beleuchtung & Steuerblöcke

- **Kinoleuchte** — 16 Helligkeitsstufen, live per verbundenem Dimmer änderbar.
- **Dimmer-Schalter** — Rechtsklick schaltet die Gruppe 0 → 4 → 8 → 12 → 15 → 0
  (Schleichen = rückwärts); Redstone AN erzwingt Licht aus, AUS stellt die gespeicherte
  Stufe wieder her. Max. 64 Leuchten pro Schalter, gleiche Dimension.
- **Projektor-Schalter** — schaltet genau einen verbundenen Projektor; Redstone AN =
  Play, AUS = aus. Erneutes Einschalten startet von vorn (Livestreams laufen live).
- **Remote-Projektorsteuerung** — öffnet die volle Projektor-GUI von überall in
  derselben Dimension (lädt nie Chunks; klare Meldung, wenn der Projektor-Chunk nicht
  geladen ist). Schleichen + Rechtsklick zeigt eine Statuszeile.
- **Kino-Werkzeug** verknüpft alles: Rechtsklick auf Leuchten → auswählen, Rechtsklick
  auf Dimmer → Gruppe verbinden; Schleichen + Rechtsklick auf Projektor → auswählen,
  Rechtsklick auf Schalter/Steuerung → verbinden; Schleichen + Rechtsklick in die
  Luft → Auswahl leeren.

### 🎫 Ticket-Schranke & 🍿 Verkaufsautomaten

- **Kinoticket**: Rollenspiel-Item (ohne eigene Funktion). An der **Ticket-Schranke**
  wird es zur Eintrittskarte: Rechtsklick mit Ticket auf die Schranke — das Ticket wird
  entwertet und die Schranke gibt einen kurzen Redstone-Puls ab (öffnet Türen/Kolben).
  Schleichen + Rechtsklick mit leerer Hand (Besitzer/Ops) öffnet die Schranken-GUI:
  erforderlichen Ticketnamen setzen (Tickets am Amboss umbenennen) oder leer lassen,
  um jedes Ticket zu akzeptieren.
- **Popcorn-Maschine / Getränkeautomat**: Rechtsklick kauft Popcorn / einen Softdrink
  (3 s Abklingzeit). Schleichen + Rechtsklick (Besitzer/Ops) öffnet die Automaten-GUI:
  ein beliebiges Item in den **Preis-Slot** ziehen — die Stackgröße ist der Preis
  (leer = kostenlos; das eigene Item wird nicht verbraucht). Zahlungen sammeln sich im
  9-Slot-Einnahmenlager; volle Kasse pausiert den Verkauf; Abbau droppt die Einnahmen.
  Käufer zahlen mit dem Stack in der Haupthand.

### 🟣 Twitch, 🖥️ Server-Side Playback, ⚙️ Konfiguration

- **Twitch-Session pro Block**: Projektor-GUI → *Twitch: anmelden...* → `auth-token`
  einfügen (Browser: twitch.tv → F12 → Cookies) für werbefreie Wiedergabe abonnierter
  Kanäle. Nur lokal gespeichert, an den Block gebunden, beim Abbau gelöscht. Das Token
  wie ein Passwort behandeln.
- **Server-Side Playback (experimentell, Opt-in)**: Der Server führt die Pipeline aus
  und verteilt einen MPEG-TS-Strom an alle Zuschauer. Aktivierung über
  `enableServerPlayback=true` in `config/cinecraft-server.properties`; ~1,2 MB/s Upload
  pro Zuschauer, 720p-Limit, automatischer Rückfall auf Client-Wiedergabe.
  Twitch-Sessions werden nie weitergegeben.
- `config/cinecraft.properties` (Client): `vlcPath`, `cookiesFromBrowser`, `extraYtDlpArgs`.
  `config/cinecraft-server.properties` (Server): `enableServerPlayback`,
  `maxServerSessions`, `streamRateKBs`, `defaultSoundRange`.
  Binaries liegen unter `<Spielordner>/cinecraft/bin/`.

### 🛠️ Crafting-Rezepte

Geformte Rezepte sind in Werkbank-Anordnung dargestellt; leere Zellen = leere Felder.

**PixelTheater-Projektor**
| | | |
|:---:|:---:|:---:|
| Glasscheibe | Glasscheibe | Glasscheibe |
| Eisenbarren | Diamant | Eisenbarren |
| Eisenbarren | Redstone | Eisenbarren |

**Kinoleuchte** (×4)
| | | |
|:---:|:---:|:---:|
| Glas | Glas | Glas |
| Glas | Glowstone | Glas |
| Eisenbarren | Eisenbarren | Eisenbarren |

**Dimmer-Schalter**
| |
|:---:|
| Eisenbarren |
| Redstone |
| Eisenbarren |

**Projektor-Schalter**
| |
|:---:|
| Eisenbarren |
| Hebel |
| Redstone |

**Remote-Projektorsteuerung**
| |
|:---:|
| Enderperle |
| Eisenbarren |
| Redstone |

**Ticket-Schranke**
| | | |
|:---:|:---:|:---:|
| Eisenbarren | Kinoticket | Eisenbarren |
| Eisenbarren | Redstone | Eisenbarren |

**Popcorn-Maschine**
| | | |
|:---:|:---:|:---:|
| Glas | Glas | Glas |
| Eisenbarren | Weizenkörner | Eisenbarren |
| Eisenbarren | Eisenbarren | Eisenbarren |

**Getränkeautomat**
| | | |
|:---:|:---:|:---:|
| Eisenbarren | Eisenbarren | Eisenbarren |
| Eisenbarren | Wassereimer | Eisenbarren |
| Eisenbarren | Eisenbarren | Eisenbarren |

**Absperrpfosten** (×2)
| |
|:---:|
| Goldnugget |
| Goldbarren |
| Goldbarren |

**Roter Teppich** (×3)
| | |
|:---:|:---:|
| Rote Wolle | Rote Wolle |

**CINEMA-Schild**
| | | |
|:---:|:---:|:---:|
| Glasscheibe | Glasscheibe | Glasscheibe |
| Glasscheibe | Glowstonestaub | Glasscheibe |
| Glasscheibe | Glasscheibe | Glasscheibe |

**Formlose Rezepte**
| Ergebnis | Zutaten |
|---|---|
| Kino-Werkzeug | Eisenbarren + Redstone + Stock |
| Kinoticket (×4) | Papier + Goldnugget |
| Popcorn (×2) | 2× Weizenkörner + Papier |
| Softdrink | Zucker + Glasflasche |
| Filmposter: Sci-Fi | 2× Papier + Blauer Farbstoff |
| Filmposter: Western | 2× Papier + Oranger Farbstoff |
| Filmposter: Horror | 2× Papier + Schwarzer Farbstoff |
| Filmposter: Romanze | 2× Papier + Rosa Farbstoff |

### ⚠️ Bekannte Einschränkungen

- Das Pausieren eines **Streams** friert Bild und Ton ein, während der Stream darunter
  weiterläuft (Live setzt am Live-Rand fort; bei Videos vergeht die Zeit während der
  Pause). Lokale Dateien pausieren exakt an der Stelle.
- „Best" ist auf 1080p begrenzt (Leinwand-Textur ist 1280×720).
- Absperrpfosten haben noch keine verbindenden Kordeln; macOS auf Apple Silicon braucht
  Homebrew-ffmpeg oder Rosetta 2; Server-Side Playback ist experimentell und
  bandbreitenintensiv.

### ⚖️ Rechtlicher Hinweis

Diese Software ist ausschließlich für Inhalte vorgesehen, für deren Wiedergabe,
Übertragung und gegebenenfalls Zwischenspeicherung die erforderlichen Rechte vorliegen.
Der Besitz eines Films, einer DVD, einer Blu-ray, einer Videodatei oder eines privaten
Streaming-Abonnements berechtigt nicht automatisch dazu, den Inhalt für andere Spieler
auf einem Minecraft-Server bereitzustellen. Illegale Streams, Film-Rips, nicht
autorisierte IPTV-Angebote sowie die Umgehung von DRM, Bezahlschranken, Werbung oder
Geo-Blocking sind nicht erlaubt. Der jeweilige Serverbetreiber ist selbst für die
verwendeten Inhalte, Quellen, Lizenzen und die Einhaltung der Anbieterbedingungen
verantwortlich. Bei öffentlichen, kommerziellen oder größeren Community-Servern wird
empfohlen, vor der Nutzung rechtlichen Rat einzuholen. Dieser Hinweis stellt keine
Rechtsberatung dar. (Rein informativ — PixelTheater enthält bewusst keine technischen
Prüf- oder Sperrmechanismen.)

### 🆕 Neu in Version 0.4.0 — „Kino-Ausstattung"

- Popcorn & Softdrinks mit Verkaufsautomaten (Item-basierte Preise, Einnahmenlager)
- Ticket-Schranke (Tickets entwerten → Redstone-Puls, optionale Namensbindung)
- Redstone-Steuerung für Projektor-Schalter und Dimmer
- Roter Teppich, Absperrpfosten, vier Filmposter, leuchtendes CINEMA-Schild, Fortschritte
- Umbenennung in PixelTheater (Autor CptGummiball); keine Änderungen an der Wiedergabe-Pipeline
- Details im [CHANGELOG.md](CHANGELOG.md)

### 🛠️ Bauen & 🐛 Fehler melden

```
./gradlew build        # Jar landet in build/libs/
./gradlew runClient    # Dev-Client
```

Fehler bitte über die GitHub-Issue-Vorlagen melden (mit `logs/latest.log` und der
getesteten URL). **Lizenz:** Apache-2.0, Copyright CptGummiball — siehe
[LICENSE](LICENSE) und [NOTICE](NOTICE); die Namensnennung der ursprünglichen
Lumière Play von jrxmod bleibt erhalten, [vlcj](https://github.com/caprica/vlcj)
ist gebündelt.
