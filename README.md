# Kingdom Rebuilt

A turn-based strategy game that combines fortress and resource management with tactical party combat. Built in Godot 4.6 with GDScript, using the GL Compatibility renderer.

Originally developed as a bachelor's thesis at the Politehnica University of Timișoara (defended 2026); a Romanian build guide is in [docs/BUILD_RO.md](docs/BUILD_RO.md).

## Gameplay

You rebuild a ruined city one turn at a time. Each turn you assign workers, upgrade buildings, recruit and train soldiers, then end the turn and deal with what comes next: enemy waves, faction events and letters from the king. Victory requires surviving 10 enemy waves, reaching dungeon level 3 and raising a set of buildings to target levels. Losing the city walls ends the run, and a lost game deletes its save (permadeath).

## Features

- **City management:** 12 buildings defined as data resources (Farm, Forest, Quarry, Iron Mine, Steel Forge, Blacksmith, Market, Butchery, Barracks, Training Grounds, Tavern, House), each with worker slots, upkeep and upgrade levels. Resources are gold, food, wood, stone, iron and steel.
- **Threat and waves:** a threat meter fills every turn and triggers an enemy wave when full. Lost waves damage walls and buildings, lower army morale and raise future threat.
- **Soldiers:** five classes (Warrior, Knight, Archer, Rogue, Mage) with levels, stat points, morale, equipment slots and three equipped skills out of five per class. Tavern staffing affects recruit quality.
- **Traits:** soldiers earn traits from what happens in battle (kills, damage taken and similar), checked after every fight.
- **Crafting:** items crafted over several turns in three quality tiers (Common, Uncommon, Rare).
- **Turn-based combat:** initiative order from speed plus a small roll, attack / defend / skill actions, critical hits, taunts, lifesteal, bosses with their own behaviour, plus auto-battle and speed toggles.
- **Procedural dungeon:** a 10x10 grid generated per level with the spawn in the centre and the boss in the farthest room; rooms include monsters, elites, fountains, trait and gear markets and lore.
- **Factions and story:** standing with three factions (Wardens, Iron Legion, Pale Court) drives passive bonuses, diplomacy actions with cooldowns and choice-based events. Story letters arrive at gameplay milestones.
- **Presentation:** animated intro cinematic, first-turn guided tutorial, in-game codex, end-of-turn recap screen, crossfading music, pooled sound effects, scene fades and a pause menu with volume settings.
- **Saves:** three save slots with autosave.

## Architecture

| Area | Location | Notes |
|---|---|---|
| Autoloads (global state) | `scripts/autoload/` | `GameState` (resources, buildings, soldiers, turns, win/loss), `CombatState` (turn order, actions, damage), `DungeonState`, `FactionState`, `FactionEvents`, `GameEvents`, `StoryManager`, `TraitChecker`, `SaveManager` |
| Autoloads (services) | `scripts/autoload/` | `Settings`, `MusicManager`, `SFX`, `SceneFader`, `PauseMenu`, `BuildingPopup` |
| Data resources | `data/buildings/*.tres`, `scripts/data/`, `scripts/resouces_data/` | `BuildingData`, `SoldierData`, `EnemyData`, `ItemData`, `SkillData`, `TraitData` as custom `Resource` classes; `SkillLibrary` and `TraitLibrary` hold the skill and trait catalogues |
| Management | `scripts/management/`, `scenes/management/` | Hub screen (city view, workers, buildings, objectives), story panel, turn recap |
| Combat | `scenes/combat/`, `scripts/combat/` | Pre-combat party selection and the battle scene (unit cards, turn order bar, log, animations) |
| Dungeon | `scripts/dungeon/`, `scenes/dungeon/` | `DungeonMap` and `DungeonRoom` generate the grid; the map scene handles exploration and room events |
| UI | `scripts/ui/`, `scenes/ui/` | Main menu, codex, tutorial, cinematic, victory and defeat overlays, shared theme and UI kit helpers |
| Tests | `test/unit/` | GUT unit tests for building, soldier, enemy and dungeon map logic |

Systems talk to each other mainly through autoload signals (for example `resources_changed`, `soldiers_changed`, `city_fallen`), so screens refresh from state instead of holding their own copies.

## How to run

1. Install Godot 4.6.x, the standard build (not .NET): [godotengine.org/download](https://godotengine.org/download).
2. Clone the repository:
   ```
   git clone https://github.com/SergiuZdr/KingdomRebuilt.git
   ```
3. Open Godot, choose **Import**, select `project.godot` in the cloned folder. The first import processes all assets.
4. Press **F5** (or Play). The game starts at the main menu.

Run the unit tests from the command line (GUT is bundled in `addons/gut`):

```
godot --headless --path . -s addons/gut/gut_cmdln.gd -gdir=res://test/unit -gexit
```

Runs on Windows, Linux and macOS. No build step is needed since GDScript is interpreted.
