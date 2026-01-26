---
name: Multiplayer Mode Requirements
overview: Add live multiplayer functionality to the French Taboo game using a simple room-code system with real-time synchronization, supporting 2-8 players with automatic team formation for 4+ players.
todos:
  - id: firebase-setup
    content: Set up Firebase Realtime Database project and add configuration to index.html
    status: completed
  - id: room-system
    content: Implement room creation, joining, and room code generation UI
    status: completed
  - id: player-management
    content: Add player list management with nicknames and colors
    status: completed
  - id: state-sync
    content: Implement real-time synchronization of game state (cards, timer, scores)
    status: completed
  - id: team-logic
    content: Add team formation and turn management for 4+ players
    status: completed
  - id: multiplayer-ui
    content: Create lobby screen and multiplayer game UI overlays
    status: completed
  - id: error-handling
    content: Add reconnection logic and graceful error handling
    status: completed
  - id: testing
    content: Test with multiple devices and update documentation
    status: completed
isProject: false
---

# Multiplayer Mode Requirements & Implementation Plan

## Overview

Add a live multiplayer mode to Taboo Français Pro that maintains the simplicity of the single-player experience while enabling multiple players to join via a simple room code system. The implementation prioritizes ease of use for users of all technical skill levels (including retirees in their 80s).

## Current Architecture Analysis

The game is currently a **single-file HTML application** (`index.html`) with:

- Pure client-side JavaScript (no build process)
- CSV word list loaded from GitHub
- Local storage for played cards
- Timer-based rounds (60 seconds)
- Score tracking per round and session

## Multiplayer Requirements

### Core Features

1. **Room System**

   - Host creates a room and receives a 4-character room code (e.g., "AB12")
   - Players join by entering the room code
   - Room shows player list with names/colors
   - Room persists until host ends it or all players leave

2. **Player Management**

   - Players enter a simple nickname (no accounts required)
   - Each player gets a unique color/avatar
   - Host can start the game when ready
   - Players can leave/join mid-session (graceful handling)

3. **Game Modes**

   - **2-3 Players**: Turn-based (one describes, others guess)
   - **4+ Players**: Team-based (automatic team split, teams alternate turns)
   - Same word pool and rules as single-player
   - Shared timer visible to all players
   - All opposing team players see the cards that the prompting player sees and they get a buzzer to buzz the prompting player
   - The guessing player sees neither cards nor buzzer, they only see the timer
   - The prompting player gets a new button called 'Buzzed' that makes the current card ineligible: it doesn't add to their score and it's taken out of the game.

4. **Real-time Synchronization**

   - Current word/card synced across all players
   - Host starts the overall game session from lobby
   - Active player (whose turn it is) starts their own round/timer
   - Timer synchronized (controlled by active prompting player)
   - Score updates in real-time
   - Skip/buzz actions visible to all
   - Round transitions synchronized (when active player finishes their turn)

5. **UI Enhancements**

   - New "Create Room" / "Join Room" buttons on start screen
   - Room lobby screen showing players
   - In-game display showing whose turn it is
   - Team indicators for team mode
   - Player scores visible during game

### Technical Approach

**Recommended: Firebase Realtime Database** (simplest, no server maintenance)

**Why Firebase:**

- No backend server to maintain
- Free tier sufficient for small-scale use
- Real-time synchronization built-in
- Simple JavaScript SDK
- Works with static hosting (GitHub Pages, Netlify, etc.)

**Alternative: Supabase** (similar benefits, open-source)

**Architecture:**

```
┌─────────────────────────────────────────┐
│         Firebase Realtime DB            │
│  ┌───────────────────────────────────┐  │
│  │  rooms/{roomCode}/                │  │
│  │    - host: "playerId"             │  │
│  │    - players: {playerId: {...}}   │  │
│  │    - gameState: {...}             │  │
│  │    - currentCard: {...}           │  │
│  │    - timer: 60                    │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
         ↕ WebSocket
┌─────────────────────────────────────────┐
│      Client 1 (Host)    Client 2-N     │
│      index.html         index.html      │
│      (same file)        (same file)     │
└─────────────────────────────────────────┘
```

### Implementation Details

#### 1. Firebase Setup

- Add Firebase SDK via CDN (no build step)
- Initialize with public config (no secrets in code)
- Use anonymous authentication or no auth (simplest)
- Structure: `rooms/{roomCode}/` with nested data

#### 2. Code Structure Changes

- Keep single-file architecture (add multiplayer code to existing `index.html`)
- Add `MultiplayerManager` class alongside `TabooPro`
- Toggle between single-player and multiplayer modes
- Minimal changes to existing game logic

#### 3. Room Code Generation

- Generate 4-character alphanumeric codes (e.g., "AB12")
- Check uniqueness in Firebase
- Display prominently with copy-to-clipboard button

#### 4. State Synchronization

- **Host controls**: Game session start (from lobby), room management
- **Active player controls**: Their own round timer start, card progression during their turn, round end
- **All players**: Current card display (when active player's turn), scores, player list
- **Event-driven**: Listen to Firebase changes, update UI reactively
- **Turn flow**: When it's a player's turn, they see "Start Round" button; other players see "Waiting for [Player Name] to start"

#### 5. Team Formation (4+ players)

- Split players into Team A and Team B automatically
- Alternate turns between teams
- Track team scores separately
- Show active team indicator

#### 6. Error Handling

- Handle disconnections gracefully (show "Player disconnected")
- Auto-reconnect logic
- Room expiration (cleanup after 1 hour of inactivity)
- Clear error messages for users

### User Experience Flow

```
Start Screen
├─ [Single Player] → Existing flow
└─ [Multiplayer]
   ├─ [Create Room] → Generate code → Lobby Screen
   │                    └─ Share code with others
   └─ [Join Room] → Enter code → Lobby Screen
                      └─ Wait for host to start

Lobby Screen
├─ Show room code (big, copyable)
├─ List of players with colors/avatars
├─ [Start Game] (host only) → Begins game session, shows first player's turn
└─ [Leave Room]

Game Screen (Multiplayer)
├─ Show whose turn it is (or active team)
├─ Active player sees: [Start Round] button → Starts their 60-second timer
├─ Other players see: "Waiting for [Player Name] to start their round"
├─ During active player's turn:
│  ├─ Active player: Card display, timer, Skip/Buzz buttons
│  ├─ Opposing players: Card display (to monitor), Buzzer button
│  └─ Guessing players: Timer only (no card, no buzzer)
├─ Player list with scores (sidebar or top)
└─ After round: Next player's turn begins (they see "Start Round" button)

Summary Screen (Multiplayer)
├─ Team scores (if team mode)
├─ Individual scores
└─ [Next Round] / [End Game]
```

### Files to Modify

1. **`index.html`**

   - Add Firebase SDK script tag
   - Add multiplayer UI screens (lobby, room code input)
   - Add `MultiplayerManager` class
   - Integrate with existing `TabooPro` class
   - Add multiplayer-specific CSS

2. **`README.md`**

   - Document multiplayer setup
   - Add Firebase configuration instructions
   - Update game rules for multiplayer

### Security Considerations

- Room codes are not secret (anyone with code can join)
- No user authentication required (simplest UX)
- Rate limiting handled by Firebase
- Input validation for player names (prevent XSS)

### Maintenance Considerations

- **Firebase free tier limits**: 100 concurrent connections, 1GB storage (sufficient for small-scale)
- **No server maintenance**: Firebase handles scaling
- **Monitoring**: Firebase console for usage/errors
- **Backup**: Word list already in CSV (no change)

### Future Enhancements (Out of Scope)

- Private rooms with passwords
- Spectator mode
- Custom word lists per room
- Chat functionality
- Player avatars/emojis

## Implementation Phases

### Phase 1: Foundation

- Set up Firebase project and configuration
- Add room creation/joining UI
- Implement basic room state synchronization

### Phase 2: Game Synchronization

- Sync current card across players
- Implement turn-based round system (active player starts their own round)
- Synchronize timer (active player-controlled)
- Handle player join/leave events
- Add "Start Round" button for active player

### Phase 3: Scoring & Teams

- Implement team formation logic
- Sync scores across players
- Add turn/team indicators

### Phase 4: Polish

- Error handling and reconnection
- UI refinements for multiplayer
- Testing with multiple devices
- Documentation updates

## Success Criteria

- ✅ Players can join a room with a 4-character code in <30 seconds
- ✅ Game state stays synchronized across all players
- ✅ Works on mobile devices (iOS Safari, Chrome Mobile)
- ✅ Handles disconnections gracefully
- ✅ No build process or server maintenance required
- ✅ Code remains in single HTML file (or minimal file structure)