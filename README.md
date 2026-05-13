# Coinbound City

![Coinbound City gameplay preview](Docs/Images/hero.png)

A third-person action prototype built in Unreal Engine 5.7. You play as a villager character running around a cartoon-styled city, collecting coins, dodging enemies, and swinging an axe at things that get too close.

This started as a learning project following tutorial material from [GorkaGames](https://www.youtube.com/@GorkaGames). I used it to get comfortable with Blueprints, character movement, basic AI, and Unreal's Enhanced Input system. It is not a finished game.

## Gameplay

You control the villager from a third-person camera. The character can walk, jump, dash, and perform melee attacks using an axe. Enemies wander the city streets and will chase you if you get close enough. Coins are scattered across the map, and a counter on the top-right corner of the screen keeps track of how many you have picked up.

The whole thing runs inside a single cartoon city level.

## Screenshots

| | |
|---|---|
| ![Enemy encounter](Docs/Images/enemy-preview.png) | ![Jumping over the street](Docs/Images/jump-preview.png) |
| Enemies with axes patrol the city streets | The character mid-jump, dodging an enemy |

![Picking up a coin](Docs/Images/coin-pickup.png)
*Walking toward a coin pickup on the sidewalk*

## What is in the project

Everything is in Blueprints. No C++ code.

The player character (`BP_ThirdPersonCharacter`) handles movement, jumping, dashing, and a two-hit axe combo. I grabbed the straw hat and axe models from Fab. Animations cover idle, walk, jump, fall loop, and landing. The enemy (`BP_EnemyAI`) reuses the same villager skeleton but has its own AI behavior -- it patrols around and chases you when you get close. Getting hit triggers a camera shake (`BP_CameraShake_Hit`), which is a small thing but it makes combat feel a lot better.

Coins use `BP_Coin` for pickup logic. There is a glow effect on them from the Realistic VFX pack. The UI widget `WB_Coins` sits in the top-right corner and shows your current count. `BP_Coins` manages spawning.

On the audio side, I set up MetaSound sources for footsteps, axe swings, hit impacts, and the dash. The main level is `Map.umap`, built on top of the Cartoon City Free environment. The template's `ThirdPersonMap` is still in the project but I do not use it.

Input runs through Enhanced Input with `IMC_Default`.

## Project structure

```
Coinbound City/
  Config/                    Engine and input configuration
  Content/
    Audio/                   Sound effects and MetaSound sources
    Blueprints/              Core gameplay Blueprints (coin, enemy, camera shake)
    Characters/
      Mannequins/            Default UE5 mannequin (unused)
      Mannequin_UE4/         UE4 mannequin (unused)
      Villager/              Player and enemy character with animations
    Cartoon_City_Free/       Environment meshes, materials, textures
    Fab/                     Marketplace assets (coin, hats, axe)
    HouseOfChangwon/         Additional environment props
    LevelPrototyping/        Prototyping materials and meshes
    Realistic_Starter_VFX_Pack_Vol2/   VFX for coin glow and similar effects
    StarterContent/          Default UE5 starter content
    ThirdPerson/
      Blueprints/            Player character and game mode
      Input/                 Enhanced Input actions and mapping
      Maps/                  Game levels
    UI/                      Coin counter widget
  Docs/Images/               Screenshots for this README
  FirstGame.uproject         Project file
```

## Opening the project

1. Install Unreal Engine 5.7 through the Epic Games Launcher.
2. Clone this repository.
3. Open `FirstGame.uproject`. The editor will ask to compile shaders on first launch, which takes a few minutes.

No additional plugins are needed beyond the defaults. The project uses the ModelingToolsEditorMode plugin (editor only) which ships with UE5.

## Controls

The project uses Enhanced Input. Default bindings:

| Action | Keyboard | Gamepad |
|---|---|---|
| Move | WASD | Left stick |
| Look | Mouse | Right stick |
| Jump | Space | Face button bottom |
| Attack | Left click | Right trigger |
| Dash | Shift | Left trigger |

## Asset credits

The Blueprint logic is mine, written while following GorkaGames tutorials.

The city environment comes from Cartoon City Free (Fab). The villager model is used for both the player and the enemies. The axe, straw hat, wizard hat, and coin models are all free downloads from Fab. VFX (the coin glow, mostly) come from Realistic Starter VFX Pack Vol 2. House of Changwon adds some extra environment props. I also left the default UE5 Starter Content in the project.

I do not own any of these assets. They are used here for learning only.

## Status

Prototype. I built it to figure out how an Unreal project fits together, from setting up a character to wiring up enemy AI to getting a UI counter on screen. I kept the scope small on purpose.

If I come back to it, I would probably add a health system, a second level, and some kind of win/lose state. No plans for that right now though.
