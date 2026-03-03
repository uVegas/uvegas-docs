---
description: >-
  Keep track of all releases, updates, and changes to the project in
  chronological order.
---

# Changelog

### \[Version 1.2.0] - Planned

{% hint style="info" %}
This version is planned for April 2026.
{% endhint %}

* Player Refactoring: All game-specific logic has been moved into `IGameSession` implementations (e.g., `BlackjackGameSession`) and is attached on table join. The Player is now framework-neutral, while RPCs, commands, and gameplay logic are encapsulated within the respective game modules (e.g., `Games/Blackjack`).
* Blackjack Splitting implemented: Players can now split up to a maximum of 3 hands.
* Planned: Replacement of the custom Tween class with a Proxy Tween layer to support third-party tween engines (e.g., DOTween, PrimeTween, LeanTween) under the hood.
* ... TBA

### \[Version 1.1.0] - Active Development

{% hint style="info" %}
This version is currently in development and will be released in **March 2026**. Here are some of the highlights.
{% endhint %}

* Starting Chips moved to `server.cfg` (default: 25,000).
* Tickrate from `server.cfg` is now correctly applied by the NetworkManager.
* Surrender is now available if enabled in `BlackjackRules`.
* Win/Loss chip text is now displayed at the table.
* Double Down, Insurance, and Surrender rules are now visible in both Lobby and Table view.
* Insurance system expanded: offer, win, and loss events including logic and voice SFX.
* Missing game events (Surrender, Double Down) are now properly dispatched (event emission only, no additional gameplay logic).
* ... TBA

### \[Version 1.0.0] - Released

* Initial release on itch.io and Unity Asset Store.

