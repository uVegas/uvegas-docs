---
description: >-
  Overview of uVegas core systems shared across all games, including player and
  table management, lobby handling, and local game state.
---

# General Features

This section covers the **core, general features** of the uVegas system that are shared across all games.\
These include player management, table management, lobby handling, and local game state management.

**Framework Note:**\
The uVegas core systems constitute the underlying **casino framework**. This framework is **independent of any specific game** and has no knowledge of Blackjack, Poker, Roulette, or Slots. All games are built **on top of this modular framework**, leveraging its networking, table spawning, player interaction, and UI management systems.

> Note: Features that are specific to a particular game - such as Blackjack rules, Poker mechanics, or Slot behaviors - are covered separately under the [**Games** ](../games/)section.

By focusing on the general systems here, you get an overview of how uVegas handles networking, table spawning, player interactions, and UI updates in a **modular, reusable way**.
