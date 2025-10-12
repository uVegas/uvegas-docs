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

**Important:** The `server.cfg` is **intended for dedicated server builds** and is **optional**.\
If the file is not present, uVegas will use the default host, port, and other network settings defined in the `VegasNetworkManager`.

After building your server, place the configuration file in the `config` folder inside the build directory to override the default values.

Example:

```ini
# config/server.cfg
host=0.0.0.0
port=7777
```

When running multiple server instances on the same machine, provide a different port for each configuration file to avoid conflicts.

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

{% tabs %}
{% tab title="Linux" %}
```
./uVegasServer.x86_64 -batchmode -nographics -logFile server.log
```
{% endtab %}

{% tab title="Windows" %}
```
./uVegasServer.exe -batchmode -nographics -logFile server.log
```
{% endtab %}
{% endtabs %}

**Notes:**

* Unity will run the server **headlessly** - no rendering or window is created.
* Mirror automatically initializes networking based on your configuration.
* Logs are written to the specified file (`server.log`), which is useful for monitoring server activity, debugging, and analyzing connections.

***

#### 📚 Reference

For advanced hosting and deployment options, refer to the official [Mirror documentation](https://mirror-networking.gitbook.io/).
