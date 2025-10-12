---
description: >-
  Explains the client-side GameManager in uVegas, responsible for local game
  state, card tracking, dealer hands, and providing data for UI rendering.
---

# Game Managment

### Overview

The **GameManager** is responsible for managing **local game state on the client**.\
It provides a centralized way to access and store data required for UI rendering and local gameplay logic, without affecting networked game state.

***

The **GameManager** is a singleton that exists on each client. Its primary responsibilities include:

* Providing access to the **local player** (`LocalPlayer`).
* Tracking the **current table** the player is participating in (`CurrentTable`).
* Maintaining the **current deck or cards** used in the game (`CurrentCards`).
* Storing the **dealer’s hand** locally for UI display (`DealerHand`).

> All data managed by the GameManager is **client-side only**. It is intended for rendering the game interface, displaying cards, hands, and dealer actions.

***

#### Key Responsibilities

* **Local Player Reference** – stores the player object representing the local client.
* **Current Table** – holds a reference to the table the player is currently in, used for UI updates.
* **Card Definitions** – maintains `CurrentCards`, a list of card definitions from the active deck. This allows the UI to display card graphics accurately.
* **Dealer Hand** – tracks the dealer’s cards for local rendering. Methods like `AddDealerCard` and `ResetDealerCards` update the local state as the game progresses.
* **Hidden Cards** – supports card hiding for gameplay mechanics (e.g., face-down dealer cards in Blackjack).

***

#### How it Works

1. When a player joins a table, the **GameManager** sets the local player and current table references.
2. The deck for the current game is loaded into `CurrentCards`, including a special hidden card for gameplay purposes.
3. All client-side UI elements (player hand, dealer hand, card images) access data from the **GameManager**.
4. The **GameManager** does **not** handle network synchronization — it relies on **Player** and **TableManager** to send and receive game state updates.

***

This structure ensures a clean separation between **server-authoritative logic** and **client-side UI/gameplay state**, making it easier to extend and maintain for multiple games like Blackjack, Poker, Roulette, or Slots.
