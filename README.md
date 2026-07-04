# RarityLock

A [Steamodded](https://github.com/Steamodded/smods) mod for Balatro that locks every Joker the game generates to a single rarity — Common, Uncommon, Rare, or Legendary.

Built for the rarity-restricted challenge series on **[NickTG](CHANNEL_URL_HERE)** — if you found this through a video, welcome! Each episode of the series runs one rarity tier:

- Commons Only — EPISODE_4_URL
- Uncommons Only — EPISODE_5_URL
- Rares Only — EPISODE_6_URL
- Legendaries Only — EPISODE_7_URL

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
    ├── RarityLock.json
    └── config.lua
```

## Configuration

Open **Mods → RarityLock → Config** in-game:

| Option | Default | What it does |
|---|---|---|
| Lock Joker rarity | On | Master toggle for the rarity lock. |
| Locked rarity | Common | Which rarity every spawned Joker becomes. |
| Allow duplicate Jokers | Off | Joker-only duplicates: owned Jokers can reappear in shops and packs. |

Changes apply immediately — including mid-run.

## Things to know (intended behavior, not bugs)

- **Everything obeys the lock.** Any card or tag that creates a Joker without forcing a specific one goes through the lock. That means with the lock enabled, **The Soul gives you a Joker of the locked rarity instead of a Legendary**, and Rare/Uncommon Tags produce the locked rarity too. This is the point of the mod — if you want The Soul to behave normally, turn the lock off first.
- Effects that spawn a *specific* Joker by name (rather than rolling one) are unaffected by the lock.
- The duplicates toggle affects **Jokers only**. It works by clearing the "already owned" record while the Joker pool is being built, so it behaves like a Showman that ignores consumables.
- **Locking to Legendary is brutal** — there are only five Legendary Jokers in the base game. Turning on duplicates is strongly recommended for Legendary runs (this is how the series episode was played).

## Compatibility

RarityLock wraps the global `create_card` and `get_current_pool` functions and always calls through to the original, so it chains cleanly with other mods that hook the same functions the same way. Conflicts are possible with mods that *replace* these functions without calling the original, or mods that also force Joker rarities — whichever loads last wins.

Tested on Steamodded 1.0.0 beta. Vanilla saves are unaffected when the mod is disabled or removed.

## How it works (for the curious / modders)

- `create_card`'s `_rarity` argument is a **roll value** (0–1), not a rarity index: ≤ 0.70 → Common, 0.70–0.95 → Uncommon, > 0.95 → Rare. Legendary uses the separate `legendary = true` flag. RarityLock injects a fixed roll value (or the legendary flag) for every Joker created without a `forced_key`.
- Duplicate culling lives in `get_current_pool`: a Joker is removed from the pool when it's marked in `G.GAME.used_jokers` *and* no Showman is in play. When duplicates are enabled, RarityLock temporarily stashes and clears `used_jokers` while the **Joker** pool is built, then restores it immediately — consumable pools are never touched.

Both mechanisms were verified against Balatro's source rather than guessed; the comments in `RarityLock.lua` document the exact behavior.

## License

[MIT](LICENSE)
