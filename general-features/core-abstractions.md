---
description: >-
  Defines the fundamental interfaces and base classes of the uVegas framework,
  providing the architectural foundation for all games and systems.
---

# Core Abstractions

### Overview

The **Core Architecture** layer defines the contracts and shared logic that power every feature in uVegas - from tables and dealers to game rules and card handling.\
It establishes a clean, modular foundation for game development, allowing each casino game (like Blackjack or Poker) to reuse, extend, or specialize these base systems.

By following a strict **interface-first** design, uVegas ensures that new games can be implemented consistently and safely while maintaining flexibility in their internal logic.

***

### Design Principles

* **Interface-Based Abstraction**\
  Every core system - such as tables, dealers, rules, and shufflers — defines an interface (`ITable`, `IDealer`, `IGameRules`, `IShuffler`, etc.) describing expected behavior and communication points.
* **Base Class Implementations**\
  Each interface has a corresponding base class (`BaseTable`, `BaseDealer`, `BaseGameRules`, etc.) that implements shared, generic logic common to all games.\
  Game-specific classes (like `BlackjackTable` or `PokerDealer`) then extend these base classes to customize their functionality.
* **Reusable Core Systems**\
  These abstractions allow game developers to build new casino games by simply providing:
  * A custom ruleset (`MyGameRules`)
  * A dealer implementation (`MyGameDealer`)
  * A table definition (`MyGameTable`)
  * Optional supporting systems (e.g. a unique shuffler, payout logic, etc.)
* **Consistency Across Games**\
  The interface-driven architecture ensures that core systems such as seat handling, table state management, or card drawing behave identically across all games.

***

### Example Structure

| Interface    | Base Class      | Purpose                                                                         |
| ------------ | --------------- | ------------------------------------------------------------------------------- |
| `ITable`     | `BaseTable`     | Defines core table behavior - seat handling, table state, and card shoe access. |
| `IDealer`    | `BaseDealer`    | Controls game flow, phase transitions, and round logic.                         |
| `IGameRules` | `BaseGameRules` | Encapsulates rule definitions such as deck count or payout ratios.              |
| `IShuffler`  | `BaseShuffler`  | Handles deterministic or random card shuffling logic.                           |

***

### Example Inheritance Diagram

```
IGameRules
   └── BaseGameRules
         ├── BlackjackRules
         ├── PokerRules
         └── SlotsRules

ITable
   └── BaseTable
         ├── BlackjackTable
         ├── PokerTable
         └── RouletteTable

IDealer
   └── BaseDealer
         ├── BlackjackDealer
         └── PokerDealer
         
IShufflerr
   └── BaseShuffler
         └── FisherYatesShuffle      
```

### Purpose in the System

The **Core Architecture** layer serves as the _contractual backbone_ of uVegas.\
By defining what every system **must** do (through interfaces) and providing default implementations (through base classes), it ensures:

* **Consistency:** Every game behaves predictably.
* **Extensibility:** New games can be added without changing the core.
* **Maintainability:** Shared logic exists in one place - not duplicated across games.
* **Flexibility:** Each game can override or extend only the behaviors it needs.

***

### Summary

The **Core Architecture** defines how all uVegas systems interconnect.\
It ensures that every game, feature, and service - from Blackjack to Poker — is built upon a common, modular foundation that is scalable, reusable, and easy to maintain.

This makes it possible to treat uVegas not just as a collection of games, but as a **true casino framework**.
