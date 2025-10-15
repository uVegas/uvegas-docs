---
description: >-
  Learn about the hardware, software, and dependencies required to run uVegas on
  both client and dedicated server environments.
---

# System Requirements

uVegas assets are built and optimized for **Unity 6.0+ (2025 LTS)** and take full advantage of its performance and networking improvements.\
All games and multiplayer components are designed to run efficiently on both **client** and **dedicated server** environments.

{% hint style="info" %}
For detailed Unity hardware requirements, please refer to the official documentation:\
[Unity 6 System Requirements →](https://docs.unity3d.com/Manual/system-requirements.html)
{% endhint %}

***

### 🖥️ Client Requirements

The client-side components (Blackjack, Poker, Roulette, Slots, etc.) run on all Unity-supported platforms and are optimized for both desktop and mobile use.

**Supported Platforms**

* Windows 10/11
* macOS (Apple Silicon & Intel)
* Linux (Ubuntu 22.04 or newer)
* iOS 15+
* Android 10+

**Recommended Minimum Specifications**

* CPU: Quad-core processor or higher
* RAM: 8 GB
* GPU: DirectX 11 / Metal compatible graphics card
* Unity Version: 6.0 (LTS) or newer

Mobile devices should meet standard Unity requirements for 3D games.

***

### 🧩 Dedicated Server Requirements

The uVegas multiplayer architecture is built on **Mirror Networking**, running in headless mode for dedicated servers.\
Servers can be hosted on both **Windows** and **Linux** operating systems.

**Supported Server Environments**

* Windows Server 2019 / 2022
* Linux (Ubuntu 22.04+, Debian 12+)
* Docker (optional, for containerized deployment)

**Recommended Minimum Specifications**

* CPU: Dual-core processor (3.0 GHz or higher)
* RAM: 4 GB (per 100 concurrent connections)
* Network: Stable broadband connection with low latency

Headless builds are fully supported via Unity’s command-line tools and Mirror’s server mode.

***

### 🔗 Dependencies

uVegas uses **Mirror Networking** for all multiplayer functionality.

* **Mirror Version:** Bundled directly with the asset to ensure compatibility.
* The included version is regularly updated to match stable Mirror releases.
* No external installation of Mirror is required - the package includes all dependencies.

Developers can check the exact Mirror version in the `Assets/uVegas/Dependencies/Mirror` folder.

***

### ✅ Summary

| Component      | Platform                            | Notes                                    |
| -------------- | ----------------------------------- | ---------------------------------------- |
| **Client**     | Windows, macOS, Linux, iOS, Android | Optimized for Unity 6 and mobile devices |
| **Server**     | Windows, Linux                      | Headless builds supported via Mirror     |
| **Dependency** | Mirror Networking                   | Bundled and version-locked for stability |

***

uVegas is designed to be **easy to deploy, modular, and scalable** - whether you host a small test environment or a large-scale multiplayer casino.
