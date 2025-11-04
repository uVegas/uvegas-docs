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

### Configuration

Server configuration parameters (such as host and port) can be overridden using the provided config file.

{% hint style="warning" %}
The `server.cfg` is **intended for dedicated server builds** and is **optional**.\
If the file is not present, uVegas will use the default host, port, and other network settings defined in the `VegasNetworkManager`.
{% endhint %}

After building your server, place the configuration file in the `config` folder inside the build directory to override the default values.

Example:

```ini
# config/server.cfg
host=0.0.0.0
port=7777
savefile=users.db
saveinterval=360
tickrate=10
```

When running multiple server instances on the same machine, provide a different port for each configuration file to avoid conflicts.

***

### Database

The uVegas dedicated server uses **LiteDB** to manage player information and chip balances during runtime, ensuring fast access and efficient synchronization for all connected clients. Alternatively, custom database implementations can be created by implementing the `IUserDatabase` interface and replacing the instance in the `NetworkManager` where the database is initialized. For persistence, the server stores the current state in a LiteDB database file (`user.db` by default). The autosave interval, in seconds, is controlled by the `saveinterval` parameter (default: 360). On startup, the server automatically loads existing data from the specified database file if it exists.

***

### Building the Server

In Unity:

1. Open **File → Build Profiles**
2. Select your target platform (Windows or Linux Server)
3. Add the **Main Scene** to the scene list
4. Click **Build**

uVegas is compatible with both **Windows** and **Linux** dedicated builds.

***

### Running the Server

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

### Reference

For advanced hosting and deployment options, refer to the official [Mirror documentation](https://mirror-networking.gitbook.io/).
