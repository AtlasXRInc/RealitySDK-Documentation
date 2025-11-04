# Creating a Custom Game Mode

This guide covers how to create a new **Game Mode Mod** in the Reality Modkit and configure its data assets, phases, and optional features.

---

## Creating the Game Mode Mod

1. Open the **Reality** dropdown menu in the Unreal Editor.  
2. Click **New Mod**.  
3. Set the **Type** to **GameMode**.  
4. From the content browser open the GameMode and in the class defaults, assign a **Data Asset** for your game mode.  
   - The data asset class must be of type **`RealityGameData`**.

---

## Setting Up the Data Asset (`RealityGameData`)

The **RealityGameData** asset defines the rules, structure, and flow of your game mode. It includes options for gameplay logic, teams, phases, and UI behavior.

### Data Asset Fields

| Field | Description |
|-------|--------------|
| **GameMode Class** | The custom game mode class you created. |
| **Voice Chat Mode** | Controls how players communicate.<br>Options:<br>• **None** – disables voice chat.<br>• **All** – everyone can communicate.<br>• **Teams Only** – only players on the same team can talk. |
| **Use Proximity** | If enabled, players can only hear nearby voices (proximity chat). |
| **Game Widget Class** | Optional. A custom UI widget that appears on the **Reality Control Device (Tablet)** alongside the built in menu. |
| **Teams** | List of team data assets. You can create as many as you need.<br>Predefined teams: **Team_Attackers** and **Team_Defenders**.<br>Each team is its own **data asset**. To add new ones, create new team data assets and include them in this list. |
| **Phases** | A list of **`RealityGamePhase`** assets defining the structure of the match (e.g., warm-up, rounds, end game).<br>Phases execute **in order** as listed. The order matters for transitions. |

---

## Game Phases

Phases define the **sequence of gameplay flow**, such as Warm-Up, Rounds, or End Game.  
Each phase is represented by a **`RealityGamePhase`** asset.

### Premade Phases

| Phase Name | Description |
|-------------|-------------|
| **Game_WarmUp** | Currently doesn't have any predefined logic. |
| **Game_PlayTDM** | Currently doesn't have any predefined logic. |
| **Game_End** | Currently doesn't have any predefined logic. |
| **Round_TDM_Buy** | Currently doesn't have any predefined logic. |
| **Round_TDM_Play** | Currently doesn't have any predefined logic. |

---

## Phase Structure

Each **RealityGamePhase** supports logic, conditions, and optional repetition.

### Default Variables

| Variable | Description |
|-----------|--------------|
| **Name** | Identifier used for reference in other Blueprints. |
| **Duration** | How long the phase lasts (in seconds). Can be infinite if conditions handle the transition. |
| **Iterations** | How many times this phase repeats before continuing to the next one. |
| **Tags** | Metadata for identifying or filtering phases. |

### Functions

Each phase exposes two overridable events:

- **OnBegin()** – Called when the phase starts.  
- **OnEnd()** – Called when the phase ends.

### Actions & Conditions

- **Actions** are objects of class `RealityFunction` (child of `UObject`) executed when a phase **begins** or **ends**.
- **Conditions** are objects of class `RealityCondition` (child of `UObject`) that control **when the phase transitions**.
- Phases can also have **time limits** or multiple **subphases**.
- You can configure:
     - A list of **OnBegin Actions**
     - A list of **OnEnd Actions**
     - A list of **Transition Conditions**

---

## Features

The **RealityFeature** class defines optional gameplay features that can be attached to your game mode.  

---

## Class Hierarchy & API Overview

### RealityGameMode

Inherits from `RealityGameModeBase`.  
Adds team logic, scoring, AI spawning, and phase updates.

**Functions & Events:**

- `AddPoint()`  
- `SetScore()`  
- `SpawnAI()`  
- `GetAvailableTeam()`  
- `GetTeam()`  
- `GetTeamFromData()`  
- `GetTeams()`  
- `GetAvailablePlayerStartByTeam()`  
- `GetTeamFromCharacter()`  
- `GetEnemyTeamFromCharacter()`  
- `GetEnemyTeamsFromCharacter()`  
- `OnUpdatePhase()`  
- `OnUpdateScore()`

---

### RealityGameModeBase

Inherits from Unreal’s base **GameMode** class.  
Provides foundational multiplayer hooks and events.

**Functions & Events:**

- `BeginGame()`  
- `EndGame()`  
- `GetPlayerStarts()`  
- `OnCharacterDie()`  
- `OnPlayerJoin()`  
- `GetData()`  
- `GetRealityGameModeBase()`  
- `OnPlayerSpawn()`