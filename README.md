# Taboo Français Pro 🇫🇷

A web-based French language learning game inspired by the classic Taboo game. Players must describe French words without using forbidden "taboo" words, making it an engaging way to practice vocabulary and communication skills.

## 🎮 How to Play

### Single Player Mode

1. **Select a Level**: Choose from A1 (Beginner), A2 (Elementary), B1 (Intermediate), or B2 (Upper Intermediate) based on your French proficiency
2. **Start a Round**: Each round lasts 60 seconds
3. **Describe the Word**: Explain the target word without using any of the 5 taboo words listed
4. **Score Points**: Earn points for each word correctly guessed
5. **Use Your Skip**: You have one skip per round if you get stuck
6. **Buzz In**: Use the buzzer button when time runs out

### Multiplayer Mode

1. **Setup**: One player creates a room and receives a 4-character room code (e.g., "AB12")
2. **Join**: Other players enter the room code and their name to join
3. **Start Game**: Host selects a level and starts the game
4. **Take Turns**: 
   - **2-3 Players**: Turn-based - one player describes, others guess
   - **4+ Players**: Team-based - teams alternate turns
5. **Active Player**: When it's your turn, click "Start Your Round" to begin your 60-second timer
6. **Opposing Players**: Can see the card and buzz if taboo words are used
7. **Guessing Players**: See only the timer (no card, no buzzer)
8. **Scoring**: Points are tracked per player/team in real-time

## ✨ Features

- **4 Difficulty Levels**: A1, A2, B1, B2 (CEFR standards)
- **1000+ French Words**: Comprehensive vocabulary covering various topics
- **Single Player Mode**: Practice on your own with timer and scoring
- **Multiplayer Mode**: Play with friends in real-time (2-8 players)
  - **Turn-Based** (2-3 players): One player describes, others guess
  - **Team-Based** (4+ players): Teams alternate turns, compete for points
  - **Room Code System**: Simple 4-character codes to join games
  - **Real-Time Sync**: Cards, timer, and scores synchronized across all players
- **Timer**: 60-second rounds with visual countdown
- **Scoring System**: Track points per round and total session score
- **Skip Function**: One skip per round for difficult words
- **Buzzer**: Fun audio buzzer with visual feedback
- **Word Review**: Review all words played during your session with links to definitions
- **Round History**: Track your performance across multiple rounds
- **Mobile-Friendly**: Responsive design optimized for mobile devices
- **Persistent Storage**: Automatically saves your player name, ID, and game history locally
- **Auto-Rejoining**: Refreshing the page won't lose your game as long as the room exists
- **No Dependencies**: Pure HTML/CSS/JavaScript - no build process required
- **"How to Play" Overlay**: Integrated instructions available directly in the main menu

## 📋 Word Categories

The game includes words from various categories:
- **Nouns**: Places, people, objects, animals, food, etc.
- **Verbs**: Action words across different tenses
- **Adjectives**: Descriptive words
- **Proper Nouns**: Famous people, places, brands, landmarks
- **Cultural References**: French culture, history, geography

## 🚀 Getting Started

### Single Player Mode

**Option 1: Direct Use**
Simply open `index.html` in your web browser. The game will automatically load the word list from the GitHub repository.

**Option 2: Local Development**
1. Clone or download this repository
2. Open `index.html` in your web browser
3. The game will fetch the word list from the remote CSV file

**Option 3: Self-Hosted**
1. Clone this repository
2. Serve the files using any web server (e.g., Python's `http.server`, Node.js `http-server`, or any web hosting service)
3. The game will work offline if you modify the `REMOTE_URL` in the code to point to a local file

### Multiplayer Mode Setup

Multiplayer mode requires Firebase Realtime Database. Follow these steps:

1. **Create a Firebase Project**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Click "Add project" and follow the setup wizard
   - Enable **Realtime Database** (not Firestore)
   - Choose your preferred region

2. **Configure Database Rules**
   - Go to Realtime Database → Rules
   - Set rules to allow read/write (for testing):
     ```json
     {
       "rules": {
         ".read": true,
         ".write": true
       }
     }
     ```
   - **Note**: For production, restrict access based on your needs

3. **Get Firebase Configuration**
   - Go to Project Settings → General
   - Scroll down to "Your apps" section
   - Click the web icon (`</>`) to add a web app
   - Copy the Firebase configuration object

4. **Update `index.html`**
   - Open `index.html` in a text editor
   - Find the `firebaseConfig` object (around line 800)
   - Replace the placeholder values with your Firebase config.
   - **Security Tip**: Restrict your API key to your specific domain in the Google Cloud Console (APIs & Services > Credentials).
     ```javascript
     const firebaseConfig = {
       apiKey: "YOUR_API_KEY",
       authDomain: "YOUR_PROJECT_ID.firebaseapp.com",
       databaseURL: "https://YOUR_PROJECT_ID-default-rtdb.firebaseio.com",
       projectId: "YOUR_PROJECT_ID",
       storageBucket: "YOUR_PROJECT_ID.appspot.com",
       messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
       appId: "YOUR_APP_ID"
     };
     ```

5. **Test Multiplayer**
   - Open `index.html` in your browser
   - Click "Multiplayer" button
   - Create a room and share the code with others
   - All players need to use the same Firebase configuration

**Firebase Free Tier Limits:**
- 100 simultaneous connections
- 1 GB storage
- 10 GB/month downloads
- Perfect for small groups and testing!

## 📁 Project Structure

```
french-taboo/
├── index.html          # Main game file (HTML, CSS, JavaScript)
├── word-list.csv       # Word database with target words and taboo words
└── README.md          # This file
```

## 🎯 Game Rules

### Single Player
- **Objective**: Describe the target word without using any taboo words
- **Time Limit**: 60 seconds per round
- **Scoring**: 1 point per correctly guessed word
- **Skips**: 1 skip per round
- **Buzzer**: Use when time expires
- **Level Selection**: Words are filtered by selected level (includes all lower levels)

### Multiplayer
- **Objective**: Same as single player, but compete with others
- **Turn System**: 
  - **2-3 Players**: One player describes, others guess (turn-based)
  - **4+ Players**: Teams alternate turns (team-based)
- **Active Player**: Starts their own 60-second round when it's their turn
- **Opposing Players**: Can see the card and buzz if taboo words are used
- **Guessing Players**: See only the timer (no card visible)
- **Buzzed Cards**: If buzzed, the card is removed from play and doesn't count toward score
- **Scoring**: Individual scores (2-3 players) or team scores (4+ players)
- **Room Limit**: Maximum 8 players per room

## 🛠️ Technical Details

- **Frontend**: Pure HTML5, CSS3, JavaScript (ES6+)
- **Styling**: Tailwind CSS (via CDN)
- **Fonts**: Google Fonts (Lexend)
- **Data Source**: CSV file hosted on GitHub
- **Audio**: Web Audio API for buzzer sound
- **Storage**: Persistent `localStorage` for player identity, game history, and words described
- **Multiplayer**: Firebase Realtime Database for real-time synchronization
  - Real-time state sync (cards, timer, scores)
  - Room-based system with 4-character codes
  - Automatic team formation for 4+ players
  - Connection handling and reconnection logic

## 📝 CSV Format

The `word-list.csv` file follows this format:
```
Target Word,Level,Type,Taboo 1,Taboo 2,Taboo 3,Taboo 4,Taboo 5
```

Example:
```
Boulangerie,A1,Nom,Pain,Croissant,Acheter,Matin,Baguette
```

## 🎨 Customization

You can customize the game by:
- Modifying `word-list.csv` to add your own words
- Adjusting the timer duration in the JavaScript code
- Changing colors and styling in the CSS section
- Modifying the number of skips allowed per round

## 📚 Educational Use

This game is perfect for:
- French language learners
- French teachers and tutors
- Language exchange groups
- French conversation practice
- Vocabulary building exercises

## 🌐 Browser Compatibility

Works on all modern browsers:
- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## 📄 License

This project is open source and available for educational use.

## 🤝 Contributing

Contributions are welcome! You can:
- Add more words to `word-list.csv`
- Improve the game mechanics
- Enhance the UI/UX
- Add new features

## 📧 Support

For issues, questions, or suggestions, please open an issue on the GitHub repository.

---

**Enjoy learning French with Taboo Français Pro!** 🎉
