# Godot Multiplayer Engineer Reference

Use this reference for Godot 4 MultiplayerAPI work: ENet/WebRTC setup, RPCs, authority models, scene replication, MultiplayerSpawner, MultiplayerSynchronizer, lobbies, and latency testing.

## Core Rules

- Treat peer ID `1` as the server in a client-server topology.
- Make the server authoritative for gameplay-critical state such as position, health, score, inventory, and item state unless a deliberate peer-authority design is documented.
- Call `set_multiplayer_authority(peer_id)` explicitly. Do not rely on defaults.
- Guard state mutations with authority checks.
- Clients send input or requests by RPC; the server validates and updates authoritative state.
- Never let `@rpc("any_peer")` mutate gameplay state without sender and plausibility validation.
- Use `MultiplayerSpawner` for dynamically spawned networked nodes.
- Use `MultiplayerSynchronizer` only for properties that truly need replication.
- Verify synchronizer property paths at scene load; invalid paths can fail silently.

## Workflow

1. Choose topology: dedicated server, listen server, peer-to-peer, or WebRTC.
2. Diagram authority per node and per gameplay state.
3. Map every RPC: caller, executor, reliability, validation, and failure behavior.
4. Build a NetworkManager Autoload for create/join/disconnect and connection signals.
5. Add MultiplayerSpawner to the world root and register spawnable scenes.
6. Add MultiplayerSynchronizer to replicated entities and keep replicated properties minimal.
7. Test with simulated 100ms and 200ms latency before considering the feature complete.

## Network Manager Template

```gdscript
extends Node

const PORT: int = 7777
const MAX_CLIENTS: int = 8

signal player_connected(peer_id: int)
signal player_disconnected(peer_id: int)
signal server_disconnected

func create_server() -> Error:
    var peer := ENetMultiplayerPeer.new()
    var error := peer.create_server(PORT, MAX_CLIENTS)
    if error != OK:
        return error
    multiplayer.multiplayer_peer = peer
    multiplayer.peer_connected.connect(_on_peer_connected)
    multiplayer.peer_disconnected.connect(_on_peer_disconnected)
    return OK

func join_server(address: String) -> Error:
    var peer := ENetMultiplayerPeer.new()
    var error := peer.create_client(address, PORT)
    if error != OK:
        return error
    multiplayer.multiplayer_peer = peer
    multiplayer.server_disconnected.connect(_on_server_disconnected)
    return OK

func disconnect_from_network() -> void:
    multiplayer.multiplayer_peer = null
```

## Secure RPC Pattern

```gdscript
@rpc("any_peer", "reliable")
func request_pick_up_item(item_id: int) -> void:
    if not multiplayer.is_server():
        return

    var sender_id := multiplayer.get_remote_sender_id()
    var player := get_player_by_peer_id(sender_id)
    if not is_instance_valid(player):
        return

    var item := get_item_by_id(item_id)
    if not is_instance_valid(item):
        return

    if player.global_position.distance_to(item.global_position) > 100.0:
        return

    _give_item_to_player(player, item)
    confirm_item_pickup.rpc(sender_id, item_id)

@rpc("authority", "reliable")
func confirm_item_pickup(peer_id: int, item_id: int) -> void:
    if multiplayer.get_unique_id() == peer_id:
        UIManager.show_pickup_notification(item_id)
```

## Spawning Pattern

```gdscript
extends Node2D

@onready var spawner: MultiplayerSpawner = $MultiplayerSpawner

func _ready() -> void:
    if not multiplayer.is_server():
        return
    NetworkManager.player_connected.connect(_on_player_connected)
    NetworkManager.player_disconnected.connect(_on_player_disconnected)

func _on_player_connected(peer_id: int) -> void:
    var player := preload("res://scenes/Player.tscn").instantiate()
    player.name = str(peer_id)
    add_child(player)
    player.set_multiplayer_authority(peer_id)

func _on_player_disconnected(peer_id: int) -> void:
    var player := get_node_or_null(str(peer_id))
    if player:
        player.queue_free()
```

## Success Metrics

- Every replicated state mutation has an authority guard.
- Every `any_peer` RPC validates sender identity and input plausibility.
- Dynamic networked nodes are spawned through the configured replication path.
- Disconnects leave no orphaned player nodes.
- The session remains playable under at least 150ms simulated latency.
