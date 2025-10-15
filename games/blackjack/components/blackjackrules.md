---
description: >-
  Defines configurable rule sets for Blackjack tables, allowing flexible
  variations such as payout ratios, dealer behavior, and player options.
---

# BlackjackRules

### Overview

The **Blackjack Rules** component provides a fully configurable rule system for Blackjack tables in _uVegas_.\
It allows you to define all relevant gameplay parameters - from dealer behavior to payout structure - through a single **ScriptableObject**.\
These rule assets can be assigned to different table prefabs to create custom game variants (e.g., “Classic 21”, “Vegas Strip”, or “High Roller” tables).

***

### Key Features

* **Modular Configuration** - Each table can have its own rule asset.
* **Authentic Gameplay** - Supports traditional Blackjack conventions such as splits, double downs, insurance, and surrender.
* **Dynamic Adjustments** - Modify rules in the Inspector without changing code.
* **Payout Customization** - Configure winnings and insurance multipliers for various styles of play.

***

### Rule Parameters

#### Hand Values

| Property             | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| `blackjackTotal`     | The total card value required for a Blackjack (default: 21). |
| `blackjackCardCount` | Number of cards that define a natural Blackjack (usually 2). |
| `bustTotal`          | Maximum value before a hand busts (typically 21).            |

#### Dealer Rules

| Property           | Description                                                        |
| ------------------ | ------------------------------------------------------------------ |
| `dealerHitsSoft17` | Determines if the dealer must hit on soft 17 (true = dealer hits). |

#### Player Options

| Property                        | Description                                      |
| ------------------------------- | ------------------------------------------------ |
| `allowDoubleDown`               | Enables the option to double down.               |
| `doubleDownOnTotalsMin` / `Max` | Range of totals eligible for doubling down.      |
| `allowSplit`                    | Allows players to split identical cards.         |
| `maxSplits`                     | Maximum number of times a player can split.      |
| `allowResplitAces`              | Whether aces can be resplit after a split.       |
| `allowInsurance`                | Enables insurance bets when dealer shows an ace. |
| `allowSurrender`                | Allows players to surrender their hand early.    |

#### Win & Payout Settings

| Property                            | Description                                       |
| ----------------------------------- | ------------------------------------------------- |
| `winPayoutUnits`                    | Standard win payout ratio (e.g., 1:1).            |
| `blackjackPayoutUnits` / `BetUnits` | Defines the Blackjack win multiplier (e.g., 3:2). |
| `insurancePayoutUnits` / `BetUnits` | Defines the insurance win multiplier (e.g., 2:1). |

***

### Usage

1. Create a new **Blackjack Rules** asset via\
   **Assets → Create → uVegas → Blackjack → Rules**.
2. Adjust the parameters as needed in the Inspector.
3. Assign the rules asset to a **Blackjack Table** prefab via the _BaseTable_ component.
4. At runtime, the server enforces the rules for all players at that table.

***

### Example Configuration

| Variant     | Dealer Hits Soft 17 | Allow Surrender | Blackjack Payout |
| ----------- | ------------------- | --------------- | ---------------- |
| Classic 21  | ✅                   | ❌               | 3:2              |
| Vegas Strip | ❌                   | ✅               | 3:2              |
| High Roller | ✅                   | ✅               | 6:5              |
