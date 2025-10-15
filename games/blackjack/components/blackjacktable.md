---
description: >-
  Server-side component that represents a fully networked Blackjack table, built
  on top of the shared BaseTable framework for seat management, betting, and
  state synchronization.
---

# BlackjackTable

### Overview

The **BlackjackTable** class defines the server authority for a single Blackjack game instance.\
It extends the generic `BaseTable`, inheriting all core functionality for seat handling, player assignment, betting, and shoe management.

Each Blackjack table exists only on the **server**, while clients receive synchronized updates through the `TableState` object, which reflects real-time information such as player seats, bets, and game status.

The table also ensures that a **BlackjackDealer** component is present, responsible for managing the game flow, card distribution, and round resolution.

***

### Core Responsibilities

* **Server Authority** - The table manages player seating, bets, and shoe handling exclusively on the server.
* **State Synchronization** - All visual and informational updates are propagated via the networked `TableState` object to ensure clients remain in sync without accessing game logic directly.
* **Seat Management** - Dynamically adds or removes players from available seats, updating both server and client state objects.
* **Bet Handling** - Processes bets through the shared `BetOnTable` logic, enforcing table limits and player balances.
* **Game Integration** - The `BlackjackTable` is lightweight and delegates gameplay flow to the `BlackjackDealer`, maintaining a clean separation between **table infrastructure** and **game mechanics**.

***

### Class Structure

#### `BlackjackTable : BaseTable`

The specialized implementation for Blackjack tables.\
It primarily overrides the abstract members of `BaseTable` and sets `GameName` to `"Blackjack"`.\
All heavy lifting (seats, bets, and shoe) is handled by the base class.

```csharp
protected override string GameName => "Blackjack";

[Server]
public override void Init(int seatCount)
{
    base.Init(seatCount);
}
```

***

### BaseTable Integration

The underlying **BaseTable** provides all core logic shared across different games:

| Feature               | Description                                                             |
| --------------------- | ----------------------------------------------------------------------- |
| **Seat Creation**     | Automatically spawns seat and seat state data for the table.            |
| **Player Join/Leave** | Handles assignment and cleanup of players in seats.                     |
| **Bet Management**    | Verifies bets against balance and table limits.                         |
| **Discard Handling**  | Manages cards moving into the discard pile and back to the shoe.        |
| **Rule Integration**  | Uses `BaseGameRules` and `TableRules` for per-table customization.      |
| **Shoe Management**   | Initializes and maintains a multi-deck shoe using the configured rules. |

***

### Server Lifecycle

1. **Initialization** - When a table is spawned, the server sets up seat data, assigns min/max bets, and initializes the shoe.
2. **Join Phase** - Players connect to the table through network commands; seats are assigned automatically.
3. **Betting Phase** - Players place bets using validated `CmdBetOnTable` calls.
4. **Gameplay Phase** - The dealer runs the game (hits, stands, busts) via the `BlackjackDealer`.
5. **Cleanup Phase** - Cards are discarded and the table resets for the next round.

***

### Integration Notes

* The `BlackjackTable` never exposes internal server data to clients - all client information flows through synchronized DTOs like `TableState` and `SeatState`.
* Other games (e.g., Poker, Roulette) will inherit from `BaseTable` in the same manner, providing their own rule and dealer logic.
* This modular design ensures that **new games can be added without modifying the networking layer**.
