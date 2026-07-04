# RarityLock

A [Steamodded](https://github.com/Steamodded/smods) mod for Balatro that locks every Joker the game generates to a single rarity — Common, Uncommon, Rare, or Legendary.

Built for the rarity-restricted challenge series on [NickTG](https://www.youtube.com/@NickTGaming) — if you found this through a video, welcome! Each episode of the series runs one rarity tier:

- [Commons Only](https://youtu.be/mpGjdjejiO4)
- [Uncommons Only](https://youtu.be/KCIUBmaKIHU)
- [Rares Only](https://youtu.be/1S_gOapfXGc)
- [Legendaries Only](https://youtu.be/d8PPthKRvpA)
## Features

- **Lock Joker rarity** — every Joker that spawns (shops, packs, tags, consumables) is forced to your chosen rarity.
- **Allow duplicate Jokers** — an optional Joker-only "Showman effect" so owned Jokers can reappear and small pools (looking at you, Legendary) never dry up. Tarots, Planets, and Spectrals keep normal no-duplicate behavior.
- In-game config tab — toggle everything from the Mods menu, no file editing. Settings persist between sessions.

## Installation

1. Install [Steamodded](https://github.com/Steamodded/smods) (version 1.0.0 beta or newer) if you haven't already.
2. Download the latest release from the [Releases](../../releases) page.
3. Extract the `RarityLock` folder into your Balatro `Mods` directory:
   - Windows: `%AppData%/Balatro/Mods/`
4. Launch the game. RarityLock appears in the Mods menu with a config tab.

Your Mods folder should look like:

```
Mods/
└── RarityLock/
    ├── RarityLock.lua
    └── RarityLock.json
```

## Configuration

Open **Mods → RarityLock → Config** in-game:

| Option | Default | What it does |
|---|---|---|
| Lock Joker rarity | On | Master toggle for the rarity lock. |
| Locked rarity | Common | Which rarity every spawned Joker becomes. |
| Allow duplicate Jokers | Off | Joker-only duplicates: owned Jokers can reappear in shops and packs. |

## Things to know (intended behavior, not bugs)

- **Everything obeys the lock.** Any card or tag that creates a Joker without forcing a specific one goes through the lock. That means with the lock enabled, **The Soul gives you a Joker of the locked rarity instead of a Legendary**, and Rare/Uncommon Tags produce the locked rarity too. This is the point of the mod — if you want The Soul to behave normally, turn the lock off first.
- The duplicates toggle affects **Jokers only**. It works by clearing the "already owned" record while the Joker pool is being built, so it behaves like a Showman that ignores consumables.
- If duplicates toggle is not selected and no unique jokers of the selected rarity are available, the default Joker will appear.

[MIT](LICENSE)
