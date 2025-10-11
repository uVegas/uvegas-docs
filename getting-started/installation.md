# Installation

uVegas assets are installed via the **Unity Package Manager** and integrate seamlessly into new or existing Unity projects.\
The setup process is straightforward and requires no modification of your existing project settings.

***

### 📦 Installation via Unity Package Manager

1. Open Unity **Package Manager** (`Window → Package Manager`).
2. Select **"My Assets"** and locate **uVegas**.
3. Click **Download** and then **Import**.
4. Unity will add all uVegas components under: Assets/uVegas/

✅ **No project settings are overwritten.**\
uVegas is fully modular and integrates cleanly into your existing Unity environment.

***

### ⚙️ Project Configuration

While uVegas does not modify your settings, certain configurations are **recommended** for proper multiplayer operation.

#### Required Unity Settings

Open **Edit → Project Settings → Player** and verify:

* **Run In Background:** ✅ Enabled\
  This ensures the client and server continue processing while not in focus, which is essential for Mirror-based multiplayer systems.
* **Auto Graphics API (Windows):** Optional\
  Can be disabled to force DirectX11/12 if compatibility issues arise.
* **Scripting Backend:** IL2CPP or Mono (depending on platform requirements)

You can find more information in the official Mirror Networking documentation:\
[Mirror Networking Documentation →](https://mirror-networking.gitbook.io/docs/)

***

### 🧩 Scene Setup

After installation, you need to add the uVegas scenes to your **Build Settings**.

1. Navigate to: Assets/uVegas/Scenes/
2. Add the following scene(s) to your Build Settings (`File → Build Settings → Scenes In Build`):

* `Main.unity`

This **Main Scene** is used for both **client** and **server** instances.\
It contains all necessary components for initialization and can be launched directly in the Unity **Play Mode** to test uVegas locally.

> 💡 Tip: You can duplicate the Main Scene for custom implementations (e.g., "Lobby" or "CustomRoom") without breaking the base multiplayer logic.

***

### 🖥️ Running in the Editor

To test uVegas locally:

1. Open the `Main` scene.
2. Press **Play** — the local client and server simulation will start automatically.
3. Use the Unity Console for live logs (Mirror messages, connection info, etc.).

For multiplayer tests, you can also **build a standalone server** using the standard Unity headless mode:

```bash
Unity.exe -batchmode -nographics -executeMethod BuildScript.PerformServerBuild
```
