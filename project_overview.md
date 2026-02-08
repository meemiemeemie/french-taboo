# Taboolingo: Project Overview

Taboolingo (formerly French Taboo) is a multi-language, real-time word game supporting both **Local (Single Device)** and **Online Multiplayer** modes. The project focuses on language learning (French/English) through a competitive and polished "Glassmorphism" interface.

## 1. Technical Architecture

-   **Frontend**: Vanilla HTML5/JavaScript with **Tailwind CSS**.
-   **Backend**: **Firebase Realtime Database** for multiplayer synchronization and state management.
-   **Data Source**: External CSV files hosted on GitHub (`french_words.csv`, `english_words.csv`).
-   **Persistence**: `StorageManager` uses `localStorage` for player profiles, game history, and word statistics to avoid early repetition.
-   **Security**: API keys are sanitized and restricted via Firebase security rules.

## 2. Major Features & Logic

### Unified Tabbed Interface
The main menu features a dynamic tabbed layout (Local vs Online) to reduce UI clutter:
- **Local Mode**: Handles level selection, timer duration, and physical device sharing.
- **Online Mode**: Manages Firebase rooms, real-time lobby synchronization, and team assignments.

### Dynamic Role-Based UI
The game engine strictly enforces UI visibility based on the player's role:
- **Describer**: Sees the card and action buttons (Correct, Skip, Buzzed).
- **Guesser**: Sees turn indicators and role-specific instructions.
- **Buzzer Duty (Opposing Team)**: Sees the card and the **Global Buzzer** button.

### Real-time Synchronization
Orchestrated via a `MultiplayerManager` class:
- **State Listeners**: Watches for changes in score, active card, current player, and buzz events.
- **Host Logic**: The creator of the room acts as the source of truth for the timer and card selection to prevent race conditions.

## 3. Notable Iterations & Refactors

-   **Word Logging & Duplicate Prevention**: Refactored `nextCard` to accept explicit statuses (`correct`, `skipped`, `buzzed`, `timeout`). Added protection logic to ensure manual actions (like a buzz) are not overwritten by automatic round-end timeouts.
-   **Indigo Glow Fix**: Systematically clearing all styling classes (`bg-*`, `text-*`) in `updateGameUI` to prevent "css ghosting" when roles change.
-   **Local/Online Consistency**: Added the "Buzzed" button to Local mode (formerly online-only) to allow tracking forbidden word events during physical play.
-   **Fair Play Leave Logic**: Implemented dynamic player count checks to ensure sessions terminate gracefully if the headcount falls below the minimum required for the mode.
-   **Windows Emoji Optimization**: Swapped generic flag emojis for a baguette emoji specifically on Windows platforms to preserve visual quality.

---
*Last updated: February 8, 2026*
