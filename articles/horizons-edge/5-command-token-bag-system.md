---
layout: page
title: "Command Token Bag System Implementation"
permalink: /articles/horizons-edge/5-command-token-bag-system.html
---

## Overview
Implement a **Bolt Action-style command token bag system** for Horizon's Edge that creates dynamic, unpredictable turn order within each round. Players contribute command tokens to a shared bag, tokens are drawn randomly to determine who acts next, enabling tactical gameplay where players cannot predict exact action sequences.

**Core Mechanic:** Random activation prevents perfect planning, rewards adaptability, and creates exciting moments when key tokens are drawn at critical times.

## Requirements

### Functional Requirements
- **Shared Token Bag**: All players' command tokens mixed into single pool at round start
- **Random Draw Activation**: Draw token → player takes immediate action → draw next token
- **Variable Command Points**: Players start with 4 tokens, can upgrade via core island improvements
- **One Action Per Token**: Each drawn token enables exactly one action (play card, build, etc.)
- **Round-Based Reset**: Empty bag triggers new round with energy generation and card draw

### Technical Requirements
- Command token pool management across multiple players (2-8 players)
- Random token draw system with fair distribution
- Integration with existing action validation (energy costs, placement rules)
- Command point upgrade system for core islands
- Proper synchronization for multiplayer gameplay

### User Experience Requirements
- Clear visual feedback for whose token was drawn
- Token count display showing remaining tokens in bag
- Player-specific command token inventory display
- Anticipation-building UI as bag empties
- Smooth transition between token draws and actions

## Current Implementation Analysis

### Existing Systems (game_manager.gd)

**Sequential Turn System** (game_manager.gd:379-397):
```gdscript
func next_turn():
    current_player_index = (current_player_index + 1) % players.size()
    if current_player_index == 0:
        turn_number += 1
        process_round_start()
```
❌ **Problem:** Simple round-robin turn order, not bag-based

**Round Start Processing** (game_manager.gd:1022-1043):
```gdscript
func process_round_start():
    for player in players:
        player.reset_energy_for_round()
        player.reset_command_tokens()
        player.generate_energy()
        player.draw_to_hand_limit()
```
✅ **Good:** Already resets command tokens per round

**Command Token Management** (player.gd:62-63, 413-418):
```gdscript
var command_tokens: int = 4
var max_command_tokens: int = 4

func reset_command_tokens():
    command_tokens = max_command_tokens

func has_command_tokens(cost: int) -> bool:
    return command_tokens >= cost

func spend_command_tokens(amount: int) -> bool:
    if command_tokens >= amount:
        command_tokens -= amount
        return true
    return false
```
✅ **Good:** Foundation exists, needs bag integration

**Action Validation** (game_manager.gd:238-276):
- Command token costs checked before card play
- Token spending integrated with energy costs
- Refund mechanisms on failed actions

## Technical Approach

### Architecture Design

**CommandTokenBag Class** (New: `game/scripts/multiplayer/command_token_bag.gd`)
- Manages shared token pool for all players
- Handles random token drawing with cryptographically secure randomness
- Tracks token ownership and remaining counts
- Emits signals for UI updates and game flow

**Integration Points:**
- **GameManager**: Orchestrates bag creation, token draws, and action phase
- **Player**: Contributes tokens to bag, receives activation notifications
- **UIOverlayManager**: Displays bag state and active player indicators

### Data Structures

**Token Representation:**
```gdscript
class CommandToken:
    var owner_player: Player
    var token_id: int  # Unique identifier for this specific token
    var display_color: Color  # Player color for visual representation
```

**Bag State:**
```gdscript
class CommandTokenBag:
    var tokens: Array[CommandToken] = []  # Current tokens in bag
    var drawn_tokens: Array[CommandToken] = []  # History for this round
    var is_empty: bool

    signal token_drawn(token: CommandToken, remaining_count: int)
    signal bag_empty()
```

### Game Flow Transformation

**Current Flow (Sequential):**
1. Round starts → Process round start for all players
2. Player 1 takes action → Next turn
3. Player 2 takes action → Next turn
4. Continue until all players have acted
5. Repeat

**New Flow (Bag-Based):**
1. **Round Start**:
   - Process round start (energy, cards)
   - Each player contributes `max_command_tokens` to bag
   - Shuffle bag thoroughly
2. **Action Phase**:
   - Draw token from bag
   - Activate token's owner player
   - Player takes ONE action
   - Repeat until bag empty
3. **Round End**:
   - Bag empty signal
   - Start new round

### Command Point Upgrades

**Core Island Upgrade System:**
- Base: 4 command tokens per round
- Upgrade Tier 1: 5 command tokens (cost: 100 resources, 10 energy)
- Upgrade Tier 2: 6 command tokens (cost: 200 resources, 20 energy)
- Maximum: 6 command tokens (prevents runaway advantage)

**Implementation:**
```gdscript
# In Player class
var max_command_tokens: int = 4
const MAX_COMMAND_TOKEN_LIMIT: int = 6

func upgrade_command_capacity():
    if max_command_tokens < MAX_COMMAND_TOKEN_LIMIT:
        max_command_tokens += 1
        return true
    return false
```

## Implementation Plan

### Phase 1: CommandTokenBag Core Class (1-2 days)

**Create `command_token_bag.gd`:**
```gdscript
extends RefCounted
class_name CommandTokenBag

signal token_drawn(player: Player, remaining: int)
signal bag_emptied()

class Token:
    var owner: Player
    var token_id: int

    func _init(p: Player, id: int):
        owner = p
        token_id = id

var tokens: Array[Token] = []
var drawn_history: Array[Token] = []
var rng: RandomNumberGenerator

func _init():
    rng = RandomNumberGenerator.new()
    rng.randomize()

func add_player_tokens(player: Player, count: int):
    for i in range(count):
        var token = Token.new(player, tokens.size())
        tokens.append(token)

func shuffle():
    tokens.shuffle()
    # Double shuffle for better randomization
    tokens.shuffle()

func draw_token() -> Token:
    if tokens.is_empty():
        bag_emptied.emit()
        return null

    var token = tokens.pop_back()
    drawn_history.append(token)
    token_drawn.emit(token.owner, tokens.size())
    return token

func is_empty() -> bool:
    return tokens.is_empty()

func get_remaining_count() -> int:
    return tokens.size()

func get_player_remaining_count(player: Player) -> int:
    var count = 0
    for token in tokens:
        if token.owner == player:
            count += 1
    return count

func clear():
    tokens.clear()
    drawn_history.clear()
```

**Testing:**
- Unit tests for token distribution fairness
- Random draw probability verification
- Edge cases: single player, max players (8)

### Phase 2: GameManager Integration (2-3 days)

**Modify `game_manager.gd`:**

**Add Bag Instance:**
```gdscript
const CommandTokenBag = preload("res://scripts/multiplayer/command_token_bag.gd")

var command_bag: CommandTokenBag = null
var active_player: Player = null  # Currently activated player (different from current_player_index)
var waiting_for_action: bool = false
```

**Replace Round Start Logic:**
```gdscript
func process_round_start():
    print("🔄 Processing round start for all players...")

    # Reset and generate resources for all players
    for player in players:
        if not player:
            continue
        player.reset_energy_for_round()
        player.reset_command_tokens()
        player.generate_energy()
        player.draw_to_hand_limit()

    # Create new command token bag
    _initialize_command_bag()

    # Start action phase by drawing first token
    _draw_next_token()

    print("✅ Round start processing complete")

func _initialize_command_bag():
    if not command_bag:
        command_bag = CommandTokenBag.new()
        command_bag.token_drawn.connect(_on_token_drawn)
        command_bag.bag_emptied.connect(_on_bag_emptied)
    else:
        command_bag.clear()

    # Add each player's command tokens to the bag
    for player in players:
        command_bag.add_player_tokens(player, player.max_command_tokens)
        print("🪙 %s contributed %d tokens to the bag" % [player.name, player.max_command_tokens])

    # Shuffle thoroughly
    command_bag.shuffle()
    print("🎲 Command bag shuffled with %d total tokens" % command_bag.get_remaining_count())

func _draw_next_token():
    if command_bag.is_empty():
        return

    var token = command_bag.draw_token()
    if token:
        active_player = token.owner
        waiting_for_action = true
        print("🎯 Token drawn: %s's turn (tokens remaining: %d)" % [active_player.name, command_bag.get_remaining_count()])
        turn_changed.emit(active_player)

func _on_token_drawn(player: Player, remaining: int):
    # Signal for UI updates
    pass

func _on_bag_emptied():
    print("🏁 Command bag empty - round complete")
    turn_number += 1
    process_round_start()
```

**Modify Action Completion:**
```gdscript
func complete_player_action(player: Player, action_type: ActionType):
    if player != active_player:
        print("⚠️ Action attempted by non-active player")
        return false

    if not waiting_for_action:
        print("⚠️ No action expected")
        return false

    waiting_for_action = false
    player_action_completed.emit(player, action_type)

    # Draw next token after brief delay (for visual feedback)
    await get_tree().create_timer(0.5).timeout
    _draw_next_token()

    return true
```

**Update Card Playing:**
```gdscript
func play_card_from_hand(player: Player, hand_index: int, context: Dictionary = {}) -> bool:
    # Verify it's this player's token activation
    if player != active_player:
        print("❌ Not your turn - current active player: %s" % (active_player.name if active_player else "None"))
        return false

    if not waiting_for_action:
        print("❌ No action available")
        return false

    # Existing card play logic...
    # [Keep all existing validation and execution]

    # On success, mark action complete
    if success:
        complete_player_action(player, ActionType.PLAY_CARD)

    return success
```

### Phase 3: Command Point Upgrade System (1-2 days)

**Core Island Upgrade Mechanics:**

**Add to Player class:**
```gdscript
const MAX_COMMAND_TOKEN_LIMIT: int = 6
const COMMAND_UPGRADE_COSTS: Array[Dictionary] = [
    {"resources": 0, "energy": 0},      # Base (4 tokens)
    {"resources": 100, "energy": 10},   # Tier 1 (5 tokens)
    {"resources": 200, "energy": 20}    # Tier 2 (6 tokens)
]

var command_token_tier: int = 0  # 0 = base, 1 = upgraded once, 2 = upgraded twice

func can_upgrade_command_capacity() -> bool:
    return max_command_tokens < MAX_COMMAND_TOKEN_LIMIT

func get_command_upgrade_cost() -> Dictionary:
    var next_tier = command_token_tier + 1
    if next_tier >= COMMAND_UPGRADE_COSTS.size():
        return {}
    return COMMAND_UPGRADE_COSTS[next_tier]

func upgrade_command_capacity() -> bool:
    if not can_upgrade_command_capacity():
        return false

    var cost = get_command_upgrade_cost()
    if cost.is_empty():
        return false

    # Check and spend resources
    if not can_afford(cost["resources"]):
        return false
    if not energy_system.get_total_energy() >= cost["energy"]:
        return false

    spend_resources(cost["resources"])
    energy_system.spend_energy_generic(cost["energy"])

    max_command_tokens += 1
    command_token_tier += 1
    print("⬆️ %s upgraded command capacity to %d tokens!" % [name, max_command_tokens])
    return true
```

**Add to GameManager:**
```gdscript
func attempt_command_upgrade(player: Player) -> bool:
    if not player:
        return false

    if player != active_player:
        print("❌ Not your turn")
        return false

    if not player.can_upgrade_command_capacity():
        print("❌ Command capacity already at maximum")
        return false

    var cost = player.get_command_upgrade_cost()
    print("💰 Command upgrade cost: %d resources, %d energy" % [cost["resources"], cost["energy"]])

    if player.upgrade_command_capacity():
        complete_player_action(player, ActionType.UPGRADE_COMMAND)
        return true

    return false
```

### Phase 4: UI Integration (2-3 days)

**Token Bag Display Component:**

**Create `ui/token_bag_display.gd`:**
```gdscript
extends PanelContainer
class_name TokenBagDisplay

@onready var total_count_label: Label = $VBox/TotalCount
@onready var player_token_grid: GridContainer = $VBox/PlayerTokens
@onready var active_player_indicator: Label = $VBox/ActivePlayer

var game_manager = null

func _ready():
    connect_to_game_manager()

func connect_to_game_manager():
    var gm = get_node_or_null("/root/Main/GameManager")
    if gm:
        game_manager = gm
        if game_manager.command_bag:
            game_manager.command_bag.token_drawn.connect(_on_token_drawn)
            game_manager.command_bag.bag_emptied.connect(_on_bag_emptied)
        game_manager.turn_changed.connect(_on_active_player_changed)

func update_display():
    if not game_manager or not game_manager.command_bag:
        return

    var bag = game_manager.command_bag
    total_count_label.text = "Tokens Remaining: %d" % bag.get_remaining_count()

    # Clear and rebuild player token counts
    for child in player_token_grid.get_children():
        child.queue_free()

    for player in game_manager.players:
        var remaining = bag.get_player_remaining_count(player)
        var label = Label.new()
        label.text = "%s: %d" % [player.name, remaining]
        label.modulate = player.color
        player_token_grid.add_child(label)

func _on_token_drawn(player: Player, remaining: int):
    update_display()

func _on_active_player_changed(player: Player):
    if player:
        active_player_indicator.text = "Active: %s" % player.name
        active_player_indicator.modulate = player.color
    update_display()

func _on_bag_emptied():
    total_count_label.text = "Round Complete!"
```

**Add to UIOverlayManager:**
- Command upgrade button in actions tab
- Token bag display panel
- Visual token draw animation
- Active player highlight with colored border

### Phase 5: Polish & Edge Cases (1-2 days)

**Edge Case Handling:**
- Single player mode: Still use bag for consistency
- Player elimination: Remove disconnected player's remaining tokens
- Action cancellation: Don't consume token if action invalid
- Simultaneous upgrades: Prevent race conditions

**Visual Polish:**
- Token draw animation with sound effect
- Player color-coded token visualization
- Bag shaking animation while drawing
- Celebration effect when high-value tokens drawn late

**Balance Testing:**
- Verify fair distribution across player counts
- Test command upgrade economy
- Ensure no runaway leader scenarios
- Validate 2-player vs 8-player dynamics

## Deliverables

### Code Files

**New Files:**
1. `game/scripts/multiplayer/command_token_bag.gd` - Core bag management class
2. `game/scripts/ui/token_bag_display.gd` - UI component for bag visualization
3. `game/scenes/ui/token_bag_display.tscn` - UI scene

**Modified Files:**
4. `game/scripts/multiplayer/game_manager.gd` - Bag integration and round flow
5. `game/scripts/multiplayer/player.gd` - Command upgrade system
6. `game/scripts/ui/ui_overlay_manager.gd` - UI integration

### Testing Deliverables
- Unit tests for CommandTokenBag fairness
- Integration tests for round flow
- Manual test scenarios for 2, 4, and 8 players
- Edge case validation tests

### Documentation Updates
- Update CLAUDE.md with bag system usage
- Document command upgrade costs
- Add turn structure flow diagram

## Dependencies

### Existing Systems Integration
- **GameManager**: Round management, action validation
- **Player**: Command token storage, upgrade tracking
- **EnergySystem**: Upgrade cost validation
- **UIOverlayManager**: Visual feedback and controls

### New System Requirements
- Random number generation (Godot's built-in RNG)
- Signal-based communication for bag events
- UI components for token display

### Prerequisites
- Existing command token foundation (player.gd:62-63)
- Action validation system (game_manager.gd:226-276)
- Round start processing (game_manager.gd:1022-1043)

## Implementation Notes

### Godot-Specific Considerations
- Use `RandomNumberGenerator` for cryptographically secure token draws
- Leverage signals for decoupled bag → UI → game flow communication
- `await get_tree().create_timer()` for visual delay between token draws
- Resource-based upgrade costs integrate with existing economy

### Performance Considerations
- Token shuffling is O(n) operation, negligible for <50 tokens
- Bag queries are O(n) for per-player counts, acceptable for 2-8 players
- UI updates only on token draw events, not per-frame

### Multiplayer Synchronization
- Bag RNG seed must synchronize across clients
- Token draw must be server-authoritative
- Action validation prevents cheating (server-side)
- UI updates derive from authoritative game state

### Balance Considerations
**Command Upgrade Economics:**
- Early upgrade (round 2-3): 100 resources expensive but +25% actions
- Late upgrade (round 5+): More affordable but game may be decided
- Maximum 6 tokens prevents dominant strategies
- Upgrade competes with generators, buildings, and cards

**Dynamic Turn Order Benefits:**
- Prevents predictable play patterns
- Rewards flexible strategic planning
- Creates exciting clutch moments
- Mitigates first-player advantage

### Potential Challenges

**Challenge 1: Player Frustration with Randomness**
- **Risk**: Players may feel unlucky with poor token draws
- **Mitigation**: Ensure upgrade path is accessible, display probabilities clearly
- **Design**: Consider "mercy rule" for consecutive draws (optional)

**Challenge 2: Analysis Paralysis**
- **Risk**: Players hesitate because they don't know when next action occurs
- **Mitigation**: Enforce turn timers (optional), encourage decisive play
- **Design**: Keep actions quick and impactful

**Challenge 3: Bag Visualization Complexity**
- **Risk**: 8 players × 6 tokens = 48 tokens hard to visualize
- **Mitigation**: Use color-coded token piles, percentage displays
- **Design**: Simple bar chart showing player token ratios

## Future Enhancements

**Advanced Features (Post-MVP):**
- **Special Tokens**: "Double Action" tokens from specific cards/buildings
- **Token Manipulation**: Cards that add/remove tokens from bag mid-round
- **Token Prediction**: Buildings that reveal upcoming token draws
- **Asymmetric Tokens**: Faction-specific token mechanics

**AI Integration:**
- AI must account for probabilistic turn order
- Monte Carlo simulation for optimal action timing
- Risk assessment based on remaining token distribution

**Analytics:**
- Track token draw distribution fairness over many games
- Identify if certain player positions have statistical advantages
- Balance command upgrade adoption rates

---

## Summary

This implementation transforms Horizon's Edge from a predictable round-robin turn structure into a dynamic Bolt Action-style activation system. The command token bag creates exciting uncertainty while maintaining strategic depth through command point upgrades and action economy management.

**Key Benefits:**
- ✅ **Tactical Unpredictability**: Players adapt to dynamic turn order
- ✅ **Strategic Depth**: Command upgrades provide meaningful economic decisions
- ✅ **Exciting Moments**: Critical token draws create memorable gameplay
- ✅ **Scalable Design**: Works smoothly from 2 to 8 players

**Estimated Development Time:** 7-12 days for full implementation and testing
