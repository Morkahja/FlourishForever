# Flourish Forever — emote vocabulary, character settings and assets

**Creator:** Babuni.dev · **Platform:** WoW: Forever interface 16001.  
**Evidence:** `FlourishForever_ActionEmotes.lua`, storage module, TOC and release records.

## What is configurable content?

This addon has **no custom prose library** and no manually authored class dialogue lines. It binds two kinds of game-provided content:

| Content | Source | Persistence |
| --- | --- | --- |
| Ability display names, IDs | Client `C_SpellBook`/legacy spellbook APIs | Config records last selected spellID and name |
| Spell cast event | `UNIT_SPELLCAST_SUCCEEDED` from client | Not stored as a log |
| Emote tokens | `EMOTE%d+_TOKEN` globals + ROAR fallback | Each configured spell has enabled token set |
| Native emote animation/chat | `DoEmote(token)` | Determined by game, not stored in addon |
| Chance and cooldown settings | Slider input | Saved by character profile |
| Last emote-fire timestamp | `GetTime()` table | **Session-only**; resets on reload/relog |

Emotes are **discoverable from the installed client** rather than hardcoded as a fixed number of choices. A client update may change how many tokens appear, which ones have a slash command, or how specific gestures display on an individual character.

The result is a single native game emote each time a configured ability's chance and cooldown conditions are met. The source calls `DoEmote(token)`; it does not generate sentences, modify spell tooltips, attach sound files or alter game combat mechanics.

## Defaults and saved profiles

The TOC has **`SavedVariables: FlourishForeverStorage`**. Its root includes a `profiles` table indexed by **player character GUID**. That choice matches the realmless Forever client identity model rather than relying on identical first names or any supposed separate-realm collision behavior.

Each profile stores:
- `actionEmotesEnabled`, default **true**.
- `instances` map keyed by a trimmed lowercase **spell name**, initially empty.
- Per instance: `name`, `spellID`, `chance` (default **100**), `cooldown` (default **6**), `emotes` enabled-token map (default **ROAR=true**).

The `instances` field name is a historical code key; it does **not** imply instance or dungeon-specific settings. Configuration is by character and ability-name, not by WoW dungeon, raid, zone or server realm.

Older `ROARitFOREVERStorage` may be adopted if already loaded. Legacy character profiles may also have been stored under plain name or name-realm keys; current code moves a matching old table to the character's GUID key when needed. Do not assume a removed addon automatically loads its old variables for migration.

**Not saved:** last emote timestamp, every cast event, a chat transcript, cooldown between logout/reloads, party-member identity, target information or cross-player communications.

## Commands and UI text

- `/flourish`, `/flourishforever`, `/rit` with `config`, `ui`, and `status`.
- Window title **Flourish Forever**.
- Labels **Enable ability emotes**, **Add ability**, **Configured abilities**, **Emotes (one is chosen at random)**, **Chance**, **Cooldown**, **Remove**.
- Status prints master enabled state, configured ability count, and a **GUID-bearing** profile reference.

The source relies on English UI strings and fallback emote labels, with game-global tokens/spell names potentially localized. There is no dedicated localization table, translated settings copy, or in-repository icon bundle.

## Content provenance and rights

The Git tree contains only **three Lua files**, a TOC, `.pkgmeta`, README, changelog and project documentation. No screenshot, sound, third-party texture, runtime dependency or test directory was found.

The original text names **Babunigaming** as the developer; October 26 metadata credited **Babuni.dev**. WoW emote animations and client assets belong to their rightsholders. **No LICENSE** exists in the current repo, so do not imply a grant of permission to reuse this code beyond applicable law.
