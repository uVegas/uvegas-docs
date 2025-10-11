---
description: >-
  Instructions for building, configuring, and launching uVegas dedicated servers
  on Windows and Linux systems.
---

# Dedicated Server

uVegas provides full support for **dedicated server hosting** based on Unity and Mirror.

The **Main Scene** (`Assets/uVegas/Scenes/Main.unity`) is the entry point for both client and server.\
When built as a **headless server**, Mirror automatically starts the server on launch.

***

#### 🔧 Configuration

Server configuration parameters (such as host and port) can be overridden using the provided config file.

**Important:** The `server.cfg` is intended for **dedicated server builds**.\
After building your server, place the configuration file in the `config` folder inside the build directory to override the default host and port.

Example:

```ini
# config/server.cfg
host=0.0.0.0
port=7777
```

***

#### 🏗️ Building the Server

In Unity:

1. Open **File → Build Settings**
2. Enable **Server Build**
3. Select your target platform (Windows or Linux)
4. Add the **Main Scene** to the build list
5. Click **Build**

uVegas is compatible with both **Windows** and **Linux** dedicated builds.

***

#### ▶️ Running the Server

**Windows (PowerShell)**

```powershell
./uVegasServer.exe -batchmode -nographics
```

**Linux (Terminal)**

```bash
./uVegasServer.x86_64 -batchmode -nographics
```

Unity will run the server headlessly — no rendering or window is created.\
Mirror automatically initializes networking based on your configuration file.

***

#### 📚 Reference

For advanced hosting and deployment options, refer to the official [Mirror documentation](https://mirror-networking.gitbook.io/).

***

> 💡 Tip: Unity generates server logs automatically (e.g., `Player.log`).\
> You can monitor these logs to verify connections, errors, and gameplay events during runtime.
