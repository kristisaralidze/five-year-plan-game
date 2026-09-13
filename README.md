# The Five Year Plan

A city-building simulation game written in C# with MonoGame. The player zones land,
builds infrastructure, balances a budget, and keeps a population happy while disasters
periodically undo the work.

Built as a university project by **Kristine Saralidze**, **Cristian Stinca**, and
**Toma Sulava-Sulaberidze**.

## Gameplay

Place residential, industrial, and service zones, then connect them with roads and
support them with facilities. Citizens move in based on what is available nearby,
satisfaction rises and falls with services and distance, and the city budget has to
absorb both construction and upkeep. Disasters damage zones, which then heal over time.

- **Zones** residential, industrial, service
- **Facilities** roads, schools, universities, police stations, stadiums
- **Systems** budget and taxation, citizen satisfaction, distance-based zone effects, disasters
- **Persistence** three save slots, written in both binary and JSON

## Architecture

The project separates concerns along Model, View, Controller, and Persistence layers.

```
Model/          Game state and rules
  City/         Map, tiles, citizens
  Zones/        Residential, Industrial, Service
  Facilities/   Roads, schools, universities, police, stadiums
  Disasters/    Disaster behaviour
  GameModel.cs  Central game state
Controller/     Input handling and game loop
View/           MonoGame rendering
Persistence/    Save and load
```

Two patterns carry most of the structure:

**Factory** Every placeable object has a matching factory (`ZoneFactory`,
`FacilityFactory`, `RoadFactory`, `SchoolFactory`, `UniversityFactory`,
`PoliceStationFactory`, `StadiumFactory`). Construction logic stays out of the game
loop, and new buildable types can be added without touching placement code.

**Singleton** `GameModel` is accessed through `GetInstance()`, so every layer reads one
authoritative game state rather than passing it through the call stack.

## Running it

Requires the .NET SDK.

```bash
dotnet restore
dotnet run
```

## Built with

C#, MonoGame Framework (DesktopGL), MonoGame.Extended

## Authors

- Kristine Saralidze
- Cristian Stinca
- Toma Sulava-Sulaberidze

## Licence

Copyright (c) 2024 Kristine Saralidze, Cristian Stinca, Toma Sulava-Sulaberidze.
All rights reserved. See [LICENSE](./LICENSE).
