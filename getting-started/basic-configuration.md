---
description: >-
  Overview of uVegas asset settings and component-specific configuration
  options.
---

# Basic Configuration

uVegas is designed to be **highly modular and customizable**. Each game component comes with its **own configuration**, allowing you to adjust behavior without modifying core scripts.

{% hint style="info" %}
uVegas comes with **default configurations** that reflect authentic casino rules and gameplay settings.\
For additional or specialized tables, you can **duplicate these default setups** and adjust parameters such as table rules, limits, card decks, and chip styles to create custom gameplay experiences.
{% endhint %}

Examples include:

* **Dealer**– Configure dealer behavior, card dealing speed, and rules.
* **Table** – Adjust table limits, blinds, and player interaction settings.

In addition to component-level settings, uVegas provides **global game settings** that apply across all assets:

* Game styles and variants
* Table rules and limits
* Card designs and deck variations
* Chips, tokens, and visual styles

All configuration files and default setups are stored in the `uVegas/Data` folder within your Unity project. This makes it easy to locate, backup, or version-control your settings. You can browse and edit these files directly if needed, while the Unity Editor provides a more convenient interface for modifying parameters on the fly.
