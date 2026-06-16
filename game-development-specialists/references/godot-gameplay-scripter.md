# Godot Gameplay Scripter Reference

Use this reference for Godot 4 gameplay architecture, GDScript 2.0, C# interop, typed signals, node composition, scene isolation, Resources, and Autoload hygiene.

## Core Rules

- Use explicit static typing in production GDScript: variables, parameters, return types, arrays, and exported properties.
- Use `:=` only when the inferred type is obvious.
- Name GDScript signals in `snake_case`; name C# signals with Godot's typed delegate pattern such as `HealthChangedEventHandler`.
- Give signals typed parameters. Avoid untyped `Variant` except for legacy interop.
- Prefer composition over inheritance. Build behavior from child components such as `HealthComponent`, `MovementComponent`, and `InteractionComponent`.
- Make every scene independently instantiable and runnable in isolation.
- Access dependencies through exported `NodePath` values or typed `@onready` references, not hardcoded sibling/parent assumptions.
- Use Autoloads only for true global services: settings, save data, event bus, input maps, network manager.
- Do not put ordinary gameplay logic in Autoloads.
- Use `_ready()` for initialization that needs the node in the tree; disconnect signals in `_exit_tree()` when needed.
- Use `queue_free()`, not `free()`, for runtime node removal.

## Workflow

1. Define self-contained scenes and root-level world scenes.
2. Map cross-scene communication through a documented EventBus Autoload.
3. Identify shared static data that belongs in `Resource` files.
4. Define typed signals before wiring systems.
5. Split monolithic scripts into focused components.
6. Audit for untyped variables, untyped arrays, raw `get_node()` calls, and accidental parent coupling.
7. Run each important scene standalone with F6-style isolation expectations.

## Typed Component Template

```gdscript
class_name HealthComponent
extends Node

## Emitted when health changes. new_health is clamped to [0, max_health].
signal health_changed(new_health: float)
signal died

@export var max_health: float = 100.0

var _current_health: float = 0.0

func _ready() -> void:
    _current_health = max_health

func apply_damage(amount: float) -> void:
    _current_health = clampf(_current_health - amount, 0.0, max_health)
    health_changed.emit(_current_health)
    if _current_health == 0.0:
        died.emit()
```

## EventBus Autoload Template

```gdscript
## Global event bus for cross-scene events only.
extends Node

signal player_died
signal score_changed(new_score: int)
signal level_completed(level_id: String)
signal item_collected(item_id: String, collector: Node)
```

## Composition Pattern

```gdscript
class_name Player
extends CharacterBody2D

@onready var health: HealthComponent = $HealthComponent
@onready var movement: MovementComponent = $MovementComponent
@onready var animator: AnimationPlayer = $AnimationPlayer

func _ready() -> void:
    health.died.connect(_on_died)
    health.health_changed.connect(_on_health_changed)

func _physics_process(delta: float) -> void:
    movement.process_movement(delta)
    move_and_slide()

func _on_died() -> void:
    animator.play("death")
    set_physics_process(false)
    EventBus.player_died.emit()

func _on_health_changed(new_health: float) -> void:
    pass
```

## Resource Data Pattern

```gdscript
class_name EnemyData
extends Resource

@export var display_name: String = ""
@export var max_health: float = 100.0
@export var move_speed: float = 150.0
@export var damage: float = 10.0
@export var sprite: Texture2D
```

## Success Metrics

- No untyped production GDScript variables or arrays.
- All signals are typed, documented, and named consistently.
- Components do not depend on parent node types.
- Scenes can run in isolation without hidden parent context.
- State changes are signal-driven where possible, not polled in `_process()`.
