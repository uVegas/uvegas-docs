---
description: >-
  Handle player spawning, state synchronization, and interactions in uVegas
  multiplayer tables.
---

# Player Management

### Overview

The **Player component** is a central element in uVegas multiplayer games.\
It represents a single player on both the server and client, ensuring that **all game logic, hand data, and player actions are synchronized correctly**.

Key features:

* **Server-authoritative spawning**
  * The `VegasNetworkManager` automatically spawns a Player prefab for each connected client.
  * This ensures that the server always has the authoritative state of all players.
* **Syncing core player data**
  * Server-controlled variables (`SyncVar`) like **username**, **balance**, and **current table** are automatically synchronized to all clients.
  * Clients also maintain **local-only variables** for gameplay purposes (e.g., hand cards, UI states).
* **Table integration**
  * Players can **join and leave tables** via commands.
  * Integration with the `TableManager` and `LobbyManager` ensures seamless seat allocation and table visibility.
  * Server-side validation prevents invalid actions and guarantees fair play.
* **Gameplay actions**
  * Players can **place bets**, interact with the table, and receive cards.
  * All updates are synchronized to other clients using Mirror’s networking RPCs.
* **UI & local state management**
  * Local variables allow the client to render hands, dealer cards, and other UI elements without constantly querying the server.
  * Hooks on `SyncVar` ensure that important changes like balance updates are reflected in the player’s UI.

***

#### Architecture Highlights

The **VegasNetworkManager** handles player connections and is responsible for spawning a **Player prefab** for each client joining the server.\
Each spawned player maintains synchronized and local data to keep gameplay consistent and responsive.

* The **server** maintains the authoritative game state and processes all player actions securely.
* The **client** renders the player’s local hand, updates the UI, and sends actions such as betting or joining tables to the server.

Each **Player prefab** includes:

* **SyncVars** for core data like username, balance, and table network ID.
* **Local variables** for data that exist only on the client side, such as the player’s hand or temporary dealer cards.
* **Commands and TargetRPCs** to manage key gameplay interactions — joining and leaving tables, placing bets, and receiving cards.

The **LobbyManager** serves as the connection layer between players and tables, allowing clients to dynamically discover available tables and join active sessions in real time.

***

> 💡 Tip: The Player prefab is universal across all uVegas games.\
> It provides a shared foundation for player data, networking, and table interaction.\
> Individual games like Blackjack, Poker, or Roulette implement their own gameplay logic on top of this shared player framework.
