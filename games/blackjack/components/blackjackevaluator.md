---
description: >-
  Core logic component that evaluates Blackjack hands, determines winners, and
  applies rule-based outcomes such as Blackjack, busts, and pushes.
---

# BlackjackEvaluator

### Overview

The **Blackjack Evaluator** is a static utility class responsible for all **hand evaluation logic** in the uVegas Blackjack system.\
It determines hand totals, detects soft and hard hands, checks for Blackjack or bust conditions, and compares player and dealer hands according to the configured **Blackjack Rules**.

This component ensures consistent and rule-driven hand evaluation across all clients and the server, making it a critical part of gameplay resolution.

***

### Core Responsibilities

* **Hand Evaluation** - Calculates total, soft/hard value, and bust status for a given hand.
* **Blackjack Detection** - Identifies a natural Blackjack based on card count and total.
* **Hand Comparison** - Compares player and dealer hands and returns the appropriate game outcome.
* **Rule Integration** — Uses parameters from `BlackjackRules` to ensure flexibility across different table configurations.

***

### Key Methods

#### `EvaluateHandValue(List<Card> hand)`

Evaluates a player or dealer hand and returns a structured `HandValue` object containing:

| Property    | Description                                             |
| ----------- | ------------------------------------------------------- |
| `Total`     | Best possible total (soft or hard) under 21.            |
| `HardTotal` | Value when counting all aces as 1.                      |
| `SoftTotal` | Value when at least one ace counts as 11 (if possible). |
| `IsSoft`    | True if hand includes an ace counted as 11.             |
| `IsBust`    | True if hand total exceeds 21.                          |

***

#### `CompareHands(List<Card> playerHand, List<Card> dealerHand, BlackjackRules rules)`

Compares player and dealer hands and returns a `HandResult`, which can be one of:

* `PlayerBlackjack`
* `DealerBlackjack`
* `PlayerWins`
* `DealerWins`
* `Push` (tie)
* `PlayerBust`
* `DealerBust`

The logic fully respects the configured **Blackjack rules**, such as `blackjackTotal` and `bustTotal`.

***

#### `HasBlackjack(List<Card> hand, BlackjackRules rules)`

Determines whether a given hand qualifies as a **natural Blackjack**,\
based on the number of cards and the target total defined in the rules.

***

### Example Usage

```csharp
var result = BlackjackEvaluator.CompareHands(player.Hand, dealer.Hand, tableRules);

if (result == HandResult.PlayerBlackjack)
    // Player Blackjack
```

***

### Integration Notes

* The evaluator is **stateless** and can safely be used both server- and client-side.
* All calculations are deterministic, ensuring consistent results across networked clients.
* It works in combination with `BlackjackRules`, `HandValue`, and `HandResult` to form the complete game evaluation pipeline.
