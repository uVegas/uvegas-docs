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

### Architecture Highlights

\[VegasNetworkManager] \
│ spawns ▼ \
\[Player Prefab] \
├─ SyncVars: username, balance, tableNetId \
├─ LocalVars: hand, dealer cards (client-side) \
└─ Commands & TargetRPCs: join table, leave table, place bet, receive cards

* **Server** maintains authoritative state.
* **Client** renders local hand, updates UI, and sends actions to the server.
* **LobbyManager** allows players to discover and join tables dynamically.

***

> 💡 Tip: Each player prefab can be customized for different games. Blackjack, Poker, Roulette, and Slot players all use the same networked Player system, but local gameplay logic is adapted per game type.
