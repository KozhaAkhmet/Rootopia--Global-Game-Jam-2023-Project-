# Rootopia

A game built in 48 hours for **Global Game Jam 2023** by a team of five (two artists, three programmers). You guide a plant's roots as they spread through obstacles toward the core of a planet.

## Gameplay

At each "divide point," a root splits into three branches (`DivideScript.Divide()` spawns a left/mid/right `Root` prefab). Enemies can sever a branch — when a `Root` collides with an object tagged `"Enemy"`, it's marked `broken` and stops growing (`Root.OnTriggerEnter2D`). If two of the three branches at a divide point are broken, the run ends (`GameState.gameOver = true`, loading the game-over scene); otherwise a new divide point spawns ahead of the one surviving branch, and the cycle continues deeper toward the core.

## Architecture

| Script | Role |
| ------ | ---- |
| `Root.cs` | A single root segment: growth, break state, and the cut animation/prefab spawned when severed |
| `DivideScript.cs` | Spawns the three child root branches at a divide point and decides the next divide point's position based on which branch survived |
| `Controller.cs` | Shared tuning constants (`timeTodivide`, a `debug` flag) |
| `GameState.cs` | Global run state (e.g. `gameOver`) |
| `MovingMobs.cs`, `TouchEgg.cs`, `MineralCollecter.cs`, `EggFinish.cs` | Enemy/obstacle and collectible behaviors |
| `LevelManager.cs`, `LevelMapManagement.cs`, `ObjectiveManager.cs` | Level flow and objectives |
| `MouseControl.cs`, `CameraMovement.cs` | Player input and camera |
| `StartManager.cs`, `DeathScreenScript.cs`, `ButtonManager.cs`, `ButtonScaling.cs` | Menu/UI flow |

## Tech Stack

Unity, C#. This repo is a fork of the original team repository (`borkluce/Rootopia--Global-Game-Jam-2023-Project-`); credit for art and level design goes to the full team.
