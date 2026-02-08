# Taboolingo: Lessons Learned & Technical Insights

This document captures the critical design decisions, technical hurdles, and strategic takeaways gained throughout the development and iteration of Taboolingo.

## 1. UI, Visuals & User Experience

### The "Indigo Glow" & Style Stacking
-   **Challenge**: In SPA development with Tailwind, simply adding a new background or text color class does not automatically remove the previous one if they are applied conditionally.
-   **Lesson**: To avoid "component ghosting" (where old styles persist, leading to unreadable combinations like dark indigo on dark indigo), always use a systematic `.classList.remove(...)` block to clear existing UI states before applying new ones.

### Micro-Instructions vs. Generic Prompts
-   **Discovery**: Player confusion was highest during role transitions. 
-   **Lesson**: Small, role-specific textual prompts (e.g., changing "Waiting..." to "Buzz if you hear a taboo word!") have a disproportionately high impact on perceived game quality. Explicitly defining user responsibility *at that exact moment* reduces friction.

### Cross-Platform Emoji Rendering
-   **Optimization**: Windows platforms often fail to render country flag emojis.
-   **Resolution**: Implemented a platform check to swap the 🇫🇷 flag for a baguette 🥖 emoji on Windows, maintaining the French theme's aesthetic charm.

## 2. Game Logic & State Management

### Word Logging Status Protection
-   **Evolution**: As word outcomes became more complex (Correct, Skipped, Buzzed, Timeout), simple binary logging failed.
-   **Bug**: Words would accidentally be logged twice (e.g., a "Buzzed" word getting logged again as "Timeout" when the round ended).
-   **Lesson**: Protective logic is essential. Final word statuses (manual skip, manual buzz, manual correct) must be "locked" so they cannot be overwritten by automated events like a timer expiration.

### Dynamic vs. Static State
-   **Challenge**: Relying on a static `initialPlayerCount` made mid-game departures break the flow.
-   **Lesson**: Critical flow decisions (like forcing a game to end) must always rely on **dynamic, real-time counters** (e.g., `Object.keys(players).length`) to remain robust against connection drops.

## 3. Multiplayer & Real-time Synchronization

### Independent Local Testing
-   **Workaround**: Testing multiplayer on one machine via multiple tabs often fails because `localStorage` is shared across instances.
-   **Solution**: Implemented a `forcePlayerId` URL parameter (e.g., `index.html?forcePlayerId=P2`) to manually assign distinct identities to each tab, enabling seamless local simulation of multiplayer interactions.

### Firebase as a State Machine
-   **Takeaway**: Real-time databases are excellent as centralized state machines but require rigorous "cleaning" on game termination.
-   **Lesson**: The `endGame` function must reset all ephemeral keys (`lastBuzz`, `roundActive`, `promptFinish`) to prevent "ghost state" when a new game starts in the same room.

---
*Documented: February 8, 2026*
