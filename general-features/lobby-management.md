---
description: >-
  Overview of the uVegas LobbyManager, showing how players discover and join
  tables. Explains network synchronization, player tracking, and dynamic lobby
  UI behavior.
---

# Lobby Management

### Overview

The **LobbyManager** is responsible for connecting players with available tables and presenting the overall casino environment.\
It acts as a bridge between the **network layer** and the **UI**, ensuring players always see up-to-date information about active tables and online users.

When the server starts, the **TableManager** spawns all configured tables.\
The **LobbyManager** keeps a synchronized list of all players and tables across the network using **Mirror’s SyncLists**.

Each connected player automatically appears in the lobby, and all available tables are displayed dynamically in the client UI.

***

#### Responsibilities

* **Player Tracking**\
  Keeps a synchronized list of all connected players.\
  Updates the total count (`playersOnline`) in real time and displays it in the lobby UI.
* **Table Listing**\
  Maintains a synchronized list of all active tables (`Tables`).\
  On the client side, a visual lobby panel is populated dynamically using `UILobbyTable` entries for each available table prefab.
* **UI Synchronization**\
  When a client connects, the lobby UI is refreshed — old entries are cleared, and all active tables are instantiated into the panel.
* **Player Join/Leave Handling**
  * Adds new players as they connect (`AddPlayer`)
  * Removes them on disconnect (`RemovePlayer`)
  * Cleans up state when the server stops

***

#### Network Flow

1. The **server** maintains authoritative lists of players and tables using Mirror SyncLists.
2. The **client** automatically synchronizes these lists and rebuilds the lobby UI.
3. When a player selects a table, the **Player** component sends a `CmdJoinTable` command to the server.
4. On success, the **UIManager** transitions from the lobby view to the corresponding game table.

***

#### Example UI Behavior

* Displays “_X Players Online_” based on the synchronized player count.
* Shows all active tables with relevant details (e.g., table type, player count).
* Automatically returns to the main menu when the connection stops.

***

#### Key Takeaways

The **LobbyManager** provides the foundation for multiplayer session discovery and entry.\
It connects the **networked backend** (Mirror) with the **visual frontend** (Unity UI), enabling players to seamlessly browse and join casino tables in real tim
