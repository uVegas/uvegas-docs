---
description: >-
  ScriptableObject-based pub/sub event system used across uVegas to decouple 
  publishers (Player) from subscribers (UIBlackjackTable).
---

# Event Management

### Overview

The `GameEvent` system is a ScriptableObject-based, decoupled event bus. Each event is a standalone asset stored under `Assets/uVegas/Data/Core/Events/`. Publishers (`Player`) raise events; subscribers (`UIBlackjackTable`) listen — neither holds a direct reference to the other.

***

### How It Works

```
GameEvent.asset  (ScriptableObject)
      │
      ├── Raise(sender, data)       ← called by Publisher
      ├── Subscribe(callback)       ← called by Subscriber
      └── Unsubscribe(callback)     ← called by Subscriber on cleanup
```

`GameEvent` internally wraps a `Action<Component, object>` C# event (`OnRaised`). All three methods delegate directly to it.

***

### 1. Creating a New GameEvent Asset

Right-click in the Project window:

```
Assets/uVegas/Data/Core/Events/
  → Create → uVegas → GameEvent
```

Name it after the moment it represents, e.g. `PlayerBust`, `DealerBlackjack`.

***

### 2. Wiring the Asset to a Publisher / Subscriber

Declare a `[SerializeField] private GameEvent` field in your `MonoBehaviour` or `NetworkBehaviour`, then assign the asset in the Inspector:

```
using uVegas.Core.Events;

[Header("Events")]
[SerializeField] private GameEvent onPlayerBustEvent;
```

> Both publisher and subscriber reference **the same asset**. That shared reference is the entire coupling mechanism.

***

### 3. Raising an Event (Publisher)

Call `Raise(Component sender, object data)` whenever the moment occurs. Pass `null` for `data` when no payload is needed:

```
// No payload
onPlayerBustEvent.Raise(this, null);

// With typed payload — cast on the subscriber side
onRevealDealerCardEvent.Raise(this, revealedCard); // revealedCard is a Card
```

`Player.cs` raises events inside client RPCs, e.g.:

```
[ClientRpc]
private void RpcOnGameOutcome(...)
{
    if (outcome == Outcome.PlayerBust)
        onPlayerBustEvent.Raise(this, null);
}
```

***

### 4. Subscribing / Unsubscribing (Subscriber)

Subscribe in `OnEnable` and unsubscribe in `OnDisable` to avoid stale callbacks or memory leaks. Callbacks must match the signature `void Handler(Component sender, object data)`.

```
private void OnEnable()
{
    onPlayerBustEvent.Subscribe(OnPlayerBust);
}

private void OnDisable()
{
    onPlayerBustEvent.Unsubscribe(OnPlayerBust);
}

private void OnPlayerBust(Component sender, object data)
{
    // sender is the Player component that raised the event
    // cast data if a payload was passed
    // e.g. Card card = (Card)data;
    ShowBustMessage();
}
```

`UIBlackjackTable.cs` follows exactly this pattern, subscribing to all relevant events in `OnEnable` and cleaning up in `OnDisable`.

***

### 5. The `GenericEvent` Enum

`GenericEvent` is a separate, plain C# `enum` under `uVegas.Core.Events`. It is **not** a ScriptableObject event. It is used as a typed discriminator for network RPCs that need to communicate mid-round moments (e.g. `TwentyOne`, `ShoeReshuffled`, `DoubleDown`) to clients, rather than as a pub/sub channel.

```
public enum GenericEvent
{
    TwentyOne,
    ShoeReshuffled,
    InsuranceOffered,
    InsuranceWon,
    InsuranceLost,
    DoubleDown,
}
```

Do not confuse it with `GameEvent`. Use `GameEvent` assets for decoupled pub/sub; use `GenericEvent` only when an RPC already handles delivery.

***

### Existing Blackjack Events

All assets live in `Assets/uVegas/Data/Core/Events/Games/Blackjack/`:

```
DealerBlackjack.asset
DealerBust.asset
DealerWin.asset
DoubleDown.asset
InsuranceLost.asset
InsuranceWon.asset
PlayerBlackjack.asset
PlayerBust.asset
PlayerReach21.asset
PlayerWin.asset
Push.asset
ReshuffleShoe.asset
RevealDealerCard.asset
Surrender.asset
```

***

### Quick Rules

| Rule                                      | Reason                                                                  |
| ----------------------------------------- | ----------------------------------------------------------------------- |
| Always unsubscribe in `OnDisable`         | Prevents callbacks on destroyed objects                                 |
| One asset = one event                     | Keep events granular and single-purpose                                 |
| Pass `null` data when no payload needed   | Keeps the API uniform                                                   |
| Cast `data` safely on the subscriber side | `data` is untyped `object`; document the expected type via XML comments |
