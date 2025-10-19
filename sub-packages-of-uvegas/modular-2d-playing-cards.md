---
description: >-
  The Modular 2D Playing Cards module provides a complete, flexible system for
  creating, managing, and displaying themeable standard playing cards in Unity.
---

# Modular 2D Playing Cards

{% hint style="info" %}
The **Modular 2D Playing Cards** module is available as a standalone asset on the Unity Asset Store for **free**. [Get it here](https://u3d.as/3G7E).
{% endhint %}

\
The **Modular 2D Playing Cards** module is the **underlying system for all playing cards in uVegas**. It offers a complete, flexible framework for card data, visuals, and UI.

### Key Components

#### Core Data Structures (`uVegas.Core.Cards`)

* **Card**\
  Represents a single playing card, storing its `Suit` and `Rank`. Includes utility functions for updating card data and generating a readable string representation.
* **Suit**\
  Enum for card suits: `Hearts`, `Diamonds`, `Clubs`, `Spades`, `Hidden`, and `Joker`.
* **Rank**\
  Enum for card ranks: `Two` through `Ace`, plus `None` (placeholder) and `Joker`.
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

{% hint style="success" %}
The module includes a **PSD file** containing all visuals for the provided themes (**Classic**, **Modern**, and **Neo**), organized in clearly labeled groups. This PSD serves as a reference and starting point for creating new themes, allowing developers to easily design custom card visuals consistent with the existing style.
{% endhint %}

### Features

* Modular architecture: data, visuals, and UI are decoupled and reusable.
* Fully themeable via `CardTheme` ScriptableObjects.
* Supports standard playing card mechanics plus jokers and hidden cards.
* UI-friendly design with hover effects, scaling, and audio.
* Easily integrates with other uVegas systems or standalone projects.

***

### Integration Notes

* The demo scene provides a **quick and easy way to test new card themes** and visualize changes in real time.
* `CardThemeManager` handles deck generation, hand drawing, and UI updates for rapid prototyping.
* Prefabs use `UICard` to display cards according to the currently selected theme.
* Card themes can be swapped **at runtime** to immediately see visual changes without modifying core data.
* Hover effects and audio in the demo are optional and can be enabled or disabled as needed.
