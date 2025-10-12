---
description: >-
  The uVegas core systems form the underlying casino framework that powers all
  games.
---

# General Features

This framework is **independent of any specific game** (Blackjack, Poker, Roulette, Slots) and provides the fundamental infrastructure needed for multiplayer casino experiences. All games are built **on top of this modular framework**, leveraging its core systems and preconfigured data.

### Core Systems

The framework includes the following general features:

* **Player Management:** Handles spawning, synchronization, and tracking of all connected players. Provides both server-authoritative state (username, balance, table assignment) and client-local data (current hand, dealer cards) for UI updates.
* **Table Management:** Responsible for spawning and managing all game tables on the server. Supports multiple table types (Blackjack, Poker, Roulette, Slots) and ensures proper seat allocation for players.
* **Lobby Management:** Displays available tables, tracks online players, and allows players to join or leave tables dynamically.
* **Local Game State Management:** Managed by the `GameManager` on the client. Stores local information such as the current table, the player's hand, dealer cards, and the active deck. Supports UI updates and local gameplay logic.

### Preconfigured Data & ScriptableObjects

uVegas comes with a set of preconfigured **ScriptableObjects** that form the data backbone of the framework. These include:

* **Cards and Decks:** Standard 52-card decks (with artwork, suits, ranks, and card backs) and configurable decks for custom rules.
* **Chips:** Predefined chip denominations with colors and values, ready to use in tables.
* **Shoes and other core data:** Supports multi-deck games and reusable definitions for all games.

These ScriptableObjects allow quick setup of tables and games while maintaining flexibility for customization. They are entirely part of the framework and can be reused across any game built on uVegas.

### Framework Independence

The core systems and data **do not depend on any specific game**. They provide:

* Networking
* Table spawning
* Player interactions
* UI updates
* Modular, reusable components for all casino games

Game-specific rules and mechanics (Blackjack rules, Poker logic, Slot behaviors, etc.) are documented separately under the [**Games**](../games/) section.

By understanding the general systems here, developers gain insight into how uVegas handles multiplayer interactions and table management in a scalable, modular way.
