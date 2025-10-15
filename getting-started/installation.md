---
description: >-
  Step-by-step guide to installing uVegas via the Unity Package Manager and
  setting up your project for multiplayer development.
---

# Installation

uVegas assets are installed via the **Unity Package Manager** and integrate seamlessly into new or existing Unity projects. The setup process is straightforward and requires no modification of your existing project settings.

***

### Unity Package Manager

1. Open Unity **Package Manager** (`Window → Package Manager`).
2. Select **My Assets** and locate the desired **uVegas package** (e.g. _uVegas Blackjack_, _uVegas Poker_, etc.).
3. Click **Download** and then **Import**.
4. Unity will add all uVegas components under: `Assets/uVegas/`

{% hint style="success" %}
**No project settings are overwritten.**\
uVegas is fully modular and integrates cleanly into your existing Unity environment.
{% endhint %}

***

### Project Configuration

While uVegas does not modify your settings, certain configurations are **recommended** for proper multiplayer operation.

#### Required Unity Settings

Open **Edit → Project Settings → Player** (Resolution and Presentation tab) and verify:

* **Run In Background:** Enabled\
  This ensures the client and server continue processing while not in focus, which is essential for Mirror-based multiplayer systems.

{% hint style="info" %}
You can find more information in the official Mirror Networking documentation:\
[Mirror Networking Documentation →](https://mirror-networking.gitbook.io/docs/)
{% endhint %}

***

### Scene Setup

After installation, you need to add the uVegas scenes to your **Build Settings**.

1. Navigate to: `Assets/uVegas/Scenes/`
2. Add the following scene(s) to your Build Settings (`File → Build Settings → Scenes In Build`):

* `Main.unity`

This **Main Scene** is used for both **client** and **server** instances.\
It contains all necessary components for initialization and can be launched directly in the Unity **Play Mode** to test uVegas locally.

***

### Running in the Editor

To test multiplayer behavior locally, uVegas supports Unity’s **Multiplayer Play Mode**.

This feature allows you to run **multiple player instances directly within the Unity Editor**, simulating both server and client connections without building separate executables.

#### Using Multiplayer Play Mode

Install the official Unity package:\
[Unity Multiplayer Play Mode →](https://docs.unity3d.com/Packages/com.unity.multiplayer.playmode@latest)

1. Open your **Main Scene** (`Assets/uVegas/Scenes/Main.unity`).
2. In the **Multiplayer Play Mode** panel, configure how many **Editor instances to open**.
3. Press **Play** to launch the configured Editor instances.
4. In each Editor instance use our custom **Mirror Network GUI** (Host, Client, or Server) to start the desired role and establish connections.

This allows you to test synchronization, gameplay logic, and table joining workflows directly within the Unity Editor - without building standalone executables.

***

### Dependencies

uVegas includes the **Mirror Networking** framework, already preconfigured for stable operation.\
The bundled version is updated regularly and pinned to a specific commit for reliability.

No additional Mirror installation is required.

***

### Summary

| Step                                | Description                                               |
| ----------------------------------- | --------------------------------------------------------- |
| **1. Install via Package Manager**  | Download and import uVegas                                |
| **2. Adjust Project Settings**      | Enable “Run in Background” and verify Unity configuration |
| **3. Add Scenes to Build Settings** | Add `Main.unity` from `Assets/uVegas/Scenes/`             |
| **4. Play in Editor**               | Test locally with integrated Mirror networking            |
| **5. (Optional)**                   | Build headless server for production use                  |

***

uVegas is designed to be **plug-and-play**, providing a clean modular structure that integrates naturally into any Unity multiplayer project - without conflicts, overrides, or unnecessary configuration.
