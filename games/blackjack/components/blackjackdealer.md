---
description: >-
  Server-authoritative game controller that manages the full round lifecycle of
  a Blackjack game — from betting to dealing, player turns, and payout
  resolution.
---

# BlackjackDealer

### Overview

The `BlackjackDealer` component defines the **server logic** for a Blackjack table.\
It controls the game flow by sequencing timed **phases**, updating **network-synced states**, and communicating all visible game events (such as dealing cards) to connected clients.

It ensures fair gameplay and consistent synchronization between players by enforcing server-side rules and managing all card draws via the shared shoe.

***

### Core Responsibilities

* 🎬 **Round Lifecycle Management** — Handles the sequence of all game phases (betting, dealing, player turns, dealer turn, resolution).
* 🂡 **Card Dealing & Visibility** — Deals cards to each seated player and to the dealer, ensuring hidden cards are correctly represented on clients.
* 🔄 **Server-Authoritative Control** — The dealer runs exclusively on the server; all actions, timers, and transitions are verified and executed there.
* 🧩 **Table Integration** — Accesses `BaseTable` to draw cards from the shoe, read seat data, and update `TableState` and `SeatState` objects.
* 🧠 **Rule Enforcement** — Uses `BlackjackRules` to validate blackjacks, busts, and payouts (including multipliers).
* 📡 **Client Synchronization** — Sends targeted Mirror RPCs to update each player’s hand, reveal cards, and synchronize visual states.

***

### Phase Lifecycle

The BlackjackDealer progresses through several **timed phases** during a round.\
Each phase is server-controlled, using coroutines to manage durations and automatic transitions.

| Phase                | Enum                            | Description                                                                          |
| -------------------- | ------------------------------- | ------------------------------------------------------------------------------------ |
| **Idle**             | `BlackjackState.Idle`           | Table is inactive; no players or game running.                                       |
| **Waiting for Bets** | `BlackjackState.WaitingForBets` | Players can place their bets before the round begins.                                |
| **Dealing**          | `BlackjackState.Dealing`        | Dealer distributes two cards to each betting player and to themselves.               |
| **Evaluate**         | `BlackjackState.Evaluate`       | Checks for natural Blackjacks before player turns begin.                             |
| **Player Turn**      | `BlackjackState.PlayerTurn`     | Each player makes decisions (hit, stand, double, split).                             |
| **Dealer Turn**      | `BlackjackState.DealerTurn`     | Dealer plays automatically according to rules (hit until 17, etc.).                  |
| **Resolution**       | `BlackjackState.Resolution`     | Winnings and losses are calculated, balances are updated, and the next round begins. |

The phase system uses the `StartPhase()` method to initialize a new state, paired with a coroutine countdown for its duration. When a timer expires, the dealer transitions automatically using `NextPhase()`.

***

### Example Flow

1. **Init** — The dealer shuffles the shoe and waits in idle mode.
2. **Betting Phase** — Once at least one player joins, the dealer starts the betting phase.
3. **Dealing Phase** — Dealer distributes two cards to each betting player and to themselves (one card hidden).
4. **Evaluation Phase** — Natural Blackjacks are detected; immediate payouts or pushes occur.
5. **Player Turns** — Each player acts within a fixed time window (hit/stand logic to be implemented).
6. **Dealer Turn** — Dealer reveals hidden card and plays according to house rules.
7. **Resolution Phase** — All hands are compared, results paid out, and the table resets for the next round.

***

### Server Integration

The dealer depends on the **BlackjackTable** for data access and state synchronization:

```csharp
[SerializeField] private BaseTable table;
```

This gives access to:

* The `Shoe` for card draws.
* The list of active `Seat` objects (each representing a player).
* The networked `TableState` for synchronized updates.
* `BlackjackRules` for rule logic (via `table.Rules`).

***

### Communication with Clients

Mirror’s **TargetRPC** calls are used to send card information and reset events to players:

* `TargetAddCardToHand()` – Adds a card to a specific player's hand.
* `TargetAddCardToDealer()` – Updates the client’s dealer hand view.
* `TargetResetPlayer()` – Resets a player’s state for the next round.

Cards are sent as network-safe `Card` structs; hidden cards are represented with\
`Suit.Hidden` and `Rank.None` until they are revealed later.

***

### Key Methods

| Method                     | Description                                                                             |
| -------------------------- | --------------------------------------------------------------------------------------- |
| `Init()`                   | Prepares the dealer, shuffles the shoe, sets initial state.                             |
| `Update()`                 | Continuously monitors player presence and phase transitions.                            |
| `StartPhase()`             | Begins a new timed phase and starts its countdown coroutine.                            |
| `PhaseTimerRoutine()`      | Coroutine that decrements the phase timer and triggers next phase when complete.        |
| `NextPhase()`              | Defines the full state machine for all Blackjack phases.                                |
| `ResetTable()`             | Resets cards and reshuffles the shoe when no players are at the table.                  |
| `EvaluateBets()`           | Checks active bets and starts the dealing routine.                                      |
| `DealCardsRoutine()`       | Sequentially deals cards to all betting players and to the dealer.                      |
| `EvaluateRoutine()`        | Handles natural Blackjack evaluation and initial payouts. _(Further expansion planned)_ |
| `SendPlayerCardToAll()`    | Sends card data for a specific player to all connected clients.                         |
| `SendDealerCardToAll()`    | Sends the dealer’s card data (hidden or revealed) to all clients.                       |
| `RevealDealerCardsToAll()` | Placeholder for revealing hidden dealer cards after evaluation.                         |
| `RevealPlayerCardsToAll()` | Placeholder for revealing hidden player cards (after Double Down, etc.).                |

***

### Summary

The **BlackjackDealer** is the **state machine** and **execution engine** of the Blackjack game.\
By keeping all logic on the **server**, and using **network-synced DTOs** for communication, it guarantees fairness and scalability across multiplayer environments.

It is designed to be **modular**, **expandable**, and reusable for other dealer-based card games (like Baccarat or Three Card Poker), by following the same `BaseTable` and `IDealer` interfaces.
