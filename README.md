# Taboo Français Pro 🇫🇷

A web-based French language learning game inspired by the classic Taboo game. Players must describe French words without using forbidden "taboo" words, making it an engaging way to practice vocabulary and communication skills. Optimized for all ages, from students to seniors.

## 🎮 How to Play

### 📱 Local Pass-and-Play (One Device)
*Best for friends and family in the same room.*

1. **Select a Level**: Choose from A1 (Beginner), A2 (Elementary), B1 (Intermediate), or B2 (Upper Intermediate).
2. **Select Timer Mode**: Choose between **Standard (60s)** or **Beginner (120s)**.
3. **Start a Round**: Click **"📱 Local Pass-and-Play"**. One person takes the phone.
4. **Describe the Word**: Explain the target word at the top without using any of the 5 taboo words listed below it.
5. **Score Points**: A teammate guesses. Click **Correct!** for each success.
6. **Pass the Phone**: After the round ends, pass the device to the next player.
6. **Buzzer**: Use the big BUZZ button if someone says a taboo word!

### 🌐 Online Multiplayer (Play from Anywhere)
*Best for playing with friends on their own devices.*

1. **Setup**: One player clicks **"🌐 Online Multiplayer"** -> "Create Room" and shares the 4-character code (e.g., "AB12").
2. **Join**: Other players enter the room code and their name to join.
3. **Start Game**: The host selects a level and **Timer Mode**, then starts the session once everyone is in.
4. **Take Turns**: 
   - **2-3 Players**: Turn-based - one player describes, the others guess.
   - **4+ Players**: Team-based - the game automatically splits you into Team A and Team B.
5. **Active Player**: When it's your turn, click **"Start Your Round"**.
6. **Buzzer Duty**: Opposing players can see your card. If they hear you say a taboo word, they'll BUZZ you!
7. **Guessing Players**: Teammates see only the timer (the card is hidden to prevent peeking).

## ✨ Features

- **4 Difficulty Levels**: A1, A2, B1, B2 (CEFR standards).
- **Variable Timers**: Choose **Standard (60s)** or **Beginner (120s)** for a more relaxed experience.
- **1000+ French Words**: Comprehensive vocabulary coverage.
- **Local Pass-and-Play**: No setup required, just one phone and a group of friends.
- **Online Multiplayer**: Play with up to 8 people in real-time.
  - **Shared Sync**: Cards, timer, and scores stay perfectly in sync.
  - **Automatic Teams**: Turns and scoring handled for you.
  - **Rejoin Logic**: Refreshing the page won't lose your spot in the game.
- **Micro-Animations**: A vibrant, premium UI that feels alive.
- **Word Review**: Full session breakdown with links to French definitions.
- **Windows Optimized**: Smart emoji detection for a great experience on any device.

## 🚀 Getting Started

### Local Mode
Simply open `index.html` in your web browser. No accounts or internet connection required (if using a local copy).

### Online Mode Setup
Multiplayer mode uses Firebase for synchronization. 

1. **Configure Firebase**: Update the `firebaseConfig` in `index.html` with your project's keys.
2. **Restrict API Key**: For security, ensure your API key is restricted to your domain in the Google Cloud Console.
3. **Launch**: Share the URL with your friends and start playing!

## 📋 Technical Details

- **Frontend**: Pure HTML5, CSS3, JavaScript (No build process).
- **Styling**: Tailwind CSS for a modern "glassmorphism" aesthetic.
- **Persistence**: `localStorage` used to remember your name and game history.
- **Real-time**: Firebase Realtime Database for multiplayer synchronization.

---

**Enjoy learning French with Taboo Français Pro!** 🎉

