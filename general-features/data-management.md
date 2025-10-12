---
description: >-
  Overview of uVegas core data represented as ScriptableObjects, including
  cards, decks, and chips, preconfigured for immediate use in any game.
---

# Data Management

### Overview

The **Data Management** system in uVegas is the central hub for all game-related assets and definitions. It leverages **Unity ScriptableObjects** to provide a flexible, modular, and easily configurable foundation for all games.

Key components include:

* **CardDefinition**: Defines a single playing card with its suit, rank, and artwork (sprite). This allows the system to render cards consistently in the UI while keeping logic and visuals separate.
* **DeckDefinition**: Represents a full deck of cards, such as a standard 52-card deck. It can include jokers, a custom card back, and exposes a method to generate a runtime list of `Card` objects for gameplay. DeckDefinitions can be duplicated or customized to create different tables or game modes.
* **Card**: The runtime representation of a card (suit + rank) used by players and the dealer. These are not ScriptableObjects but are generated from the deck definitions at runtime.
* **ChipDefinition**: Defines individual chip types, including name, value, and color. These definitions are used to generate `Chip` objects at runtime, allowing players to bet and track their currency visually and programmatically.
* **Chip**: The runtime representation of a chip, instantiated from its corresponding `ChipDefinition`.

uVegas ships with **preconfigured ScriptableObjects** for immediate use, including a full standard 52-card deck and a range of chip denominations from 1 to 5,000. This allows developers to start with authentic, ready-to-use game data while retaining the flexibility to add new decks, chip sets, or even custom card backs and themes.

By centralizing game data in ScriptableObjects, uVegas ensures a **clear separation between data and runtime logic**, making it easier to maintain, extend, and reuse assets across multiple games like Blackjack, Poker, Roulette, and Slots.

