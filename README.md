# Flourish Forever

**Flourish Forever plays an emote when you cast an ability you choose.**

Pick abilities from your spellbook, then set the chance, the cooldown, and which emotes can play. When that ability lands, one of the checked emotes is chosen at random.

Built by **Babunigaming** for **World of Warcraft: Forever** (Interface 16001).  
Current version: **0.3.1-beta**

## What it does

- Turn ability emotes on or off for the character you are playing.
- Add an ability from your spellbook. Passives are left out.
- Set the chance from 0% to 100%, and the cooldown from 0 to 120 seconds.
- Check the emotes that ability may use. One checked emote plays at random.
- Remove an ability when you no longer want it.

Each character keeps their own abilities, chances, and cooldowns.

## Commands

| Command | Purpose |
|---|---|
| `/flourish` | Open or close the window. |
| `/flourish config` | Open or close the window. |
| `/flourish status` | Show whether ability emotes are on, and how many abilities are configured. |
| `/flourishforever` | Same commands as `/flourish`. |

## Installation

Copy the `FlourishForever` folder into:

```text
Interface/AddOns/FlourishForever
```

The folder should contain `FlourishForever.toc` and the Lua files next to it. Restart WoW and enable **Flourish Forever** in the addon list.

## Release notes

See [CHANGELOG.md](CHANGELOG.md).
