---
description: >-
  Manage and spawn all tables in your uVegas multiplayer casino project,
  including Blackjack, Poker, Roulette, and Slots.
---

# Table Management

### Overview

The **TableManager** is a core component in uVegas that handles **spawning and managing all tables on the server**.\
It is designed to be **generic**, so it can manage different types of table prefabs (Blackjack, Poker, Roulette, and Slots) in a unified way.

***

### How It Works

* The `TableManager` exists as a **singleton network object** in your scene.
* It contains a **list of `TableSpawnData`** entries, each defining:
  * `tablePrefab` – the prefab to spawn (e.g., BlackjackTable, PokerTable)
  * `maxTables` – the maximum number of tables of this type
  * `maxSeats` – number of seats per table
* When the server starts (`OnStartServer`), it **spawns all configured tables** automatically.
* Each table is instantiated, initialized with its seat count, and spawned on the network using **Mirror's `NetworkServer.Spawn`**.
* After spawning, the table is **registered with the `LobbyManager`**, which allows players to see and join it.

***

### Table Prefabs

* Each table prefab must implement the `BaseTable` interface, which handles:
  * Seat allocation
  * Game initialization
  * Player interaction
* You can mix and match **different table types**:
  * Blackjack tables
  * Poker tables
  * Roulette tables
  * Slot machines (based on the same table logic)

***

### Integration with Lobby

* The `LobbyManager` keeps track of all active tables.
* Players use the lobby to **join available tables**, without needing to manually reference the spawned prefabs.
* This ensures **scalable multiplayer table management** and seamless integration with any uVegas game module.

***

> 💡 Tip: Configure your tables in the `TableManager` prefab before starting the server. Each `TableSpawnData` entry allows you to define **how many tables of each type** and **how many seats** each table supports.
