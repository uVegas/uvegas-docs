# Modular 2D Playing Cards

The **Modular 2D Playing Cards** module provides a complete, flexible system for representing and displaying standard playing cards in Unity. It includes core card data structures, visual theming, and UI integration. The module is fully modular: each component can be used individually or together as part of the uVegas ecosystem.

### Key Components

#### Core Data Structures (`uVegas.Core.Cards`)

* **Card**\
  Represents a single playing card, storing its `Suit` and `Rank`. Includes utility functions for updating card data and generating a readable string representation.
* **Suit**\
  Enum for card suits: `Hearts`, `Diamonds`, `Clubs`, `Spades`, `Hidden`, and `Joker`.
* **Rank**\
  Enum for card ranks: `Two` through `Ace`, plus `None` (placeholder) and `Joker`.
* **RankEntry**\
  Serializable struct mapping a `Rank` to its visual `Sprite`.
* **SuitEntry**\
  Serializable struct mapping a `Suit` to its visual `Sprite` and `Color`.
* **CardTheme**\
  ScriptableObject that defines the visual theme of cards, including base images, rank and suit sprites, and colors. Provides methods `GetRank(Rank)` and `GetSuit(Suit)` for runtime retrieval of visuals.

***

#### UI Integration (`uVegas.UI`)

* **UICard**\
  Handles the visual representation of a card in the UI. Uses a `CardTheme` to render the card's base, rank, and suit sprites. Supports:
  * Hidden cards (face down)
  * Joker cards
  * Dynamic theme updates
  * Runtime card reveals

***

#### Demo & Interaction (`uVegas.Demo`)

* **CardHoverEffect**\
  Adds a smooth scale and rotation animation when the player hovers over a card, including optional audio feedback.
* **CardThemeManager**\
  Manages card decks, themes, and UI presentation in demo scenes. Features:
  * Deck generation including hidden and joker cards
  * Hand drawing and randomization
  * Theme and card size selection
  * Sound effects for hover, click, select, and win events
  * Evaluates hands for simple patterns (pairs, three/four of a kind, straights) for demonstration purposes

***

### Features

* Modular architecture: data, visuals, and UI are decoupled and reusable.
* Fully themeable via `CardTheme` ScriptableObjects.
* Supports standard playing card mechanics plus jokers and hidden cards.
* UI-friendly design with hover effects, scaling, and audio.
* Easily integrates with other uVegas systems or standalone projects.

***

### Integration Notes

* Prefabs use `UICard` to display each card visually.
* `CardThemeManager` can be used to quickly prototype card-based scenes.
* Themes can be swapped at runtime without modifying core data.
* Hover effects and audio are optional and can be removed if desired.

***

### Availability

This module is part of the **uVegas** asset but is also available independently as a separate asset on the Unity Asset Store.
