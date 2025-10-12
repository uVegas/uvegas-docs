---
description: >-
  uVegas UI system separates server logic from client interfaces, using
  TableState and modular UI components for safe and scalable multiplayer UI.
---

# UI Management

### Overview

The uVegas UI system is designed to **separate game logic from client-side presentation**. Unlike the server-managed objects (e.g., `BlackjackTable`), the UI never has direct access to the game logic or internal table data. Instead, uVegas uses **TableState** objects, which are synchronized with clients and provide all necessary information for the UI to display the current game state. This ensures that the client cannot accidentally modify server-side logic and maintains server authority over gameplay.

### Core Concepts

* **UIManager:** A central singleton that manages main UI panels (menu, lobby, and game-specific interfaces). Responsible for updating global UI elements like username and player balance, and for showing or hiding the relevant panels.
* **Independent UI Components:** Game-specific UI elements (e.g., Blackjack hand displays, table panels) are designed to be self-contained. Once initialized, they automatically update based on the current TableState and do not rely on external singletons or direct references to the server objects.
* **TableState:** Represents the networked state of a table, including table ID, name, seat information, betting limits, and game-specific states (like `BlackjackState`). All UI updates are driven by this state rather than the server-side table object, maintaining a clean separation between server authority and client display.

### Advantages

* **Server-authoritative:** The UI only receives synced state data and never modifies core game logic.
* **Modular and Reusable:** Independent UI components can be reused across different tables and games without modification.
* **Safe and Flexible:** The client UI can show any information it needs while the server retains full control of gameplay, rules, and player interactions.
* **Ease of Integration:** Adding new games or tables requires minimal changes to the UI system; only new TableStates and UI components need to be implemented.

By following this architecture, uVegas ensures **secure, modular, and scalable UI management** for multiplayer casino games.
