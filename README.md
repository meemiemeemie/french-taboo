# Taboo Français Pro 🇫🇷

A web-based French language learning game inspired by the classic Taboo game. Players must describe French words without using forbidden "taboo" words, making it an engaging way to practice vocabulary and communication skills.

## 🎮 How to Play

1. **Select a Level**: Choose from A1 (Beginner), A2 (Elementary), B1 (Intermediate), or B2 (Upper Intermediate) based on your French proficiency
2. **Start a Round**: Each round lasts 60 seconds
3. **Describe the Word**: Explain the target word to your teammates without using any of the 5 taboo words listed
4. **Score Points**: Earn points for each word correctly guessed
5. **Use Your Skip**: You have one skip per round if you get stuck
6. **Buzz In**: Use the buzzer button when someone uses a taboo word or when time runs out

## ✨ Features

- **4 Difficulty Levels**: A1, A2, B1, B2 (CEFR standards)
- **1000+ French Words**: Comprehensive vocabulary covering various topics
- **Timer**: 60-second rounds with visual countdown
- **Scoring System**: Track points per round and total session score
- **Skip Function**: One skip per round for difficult words
- **Buzzer**: Fun audio buzzer with visual feedback
- **Word Review**: Review all words played during your session with links to definitions
- **Round History**: Track your performance across multiple rounds
- **Mobile-Friendly**: Responsive design optimized for mobile devices
- **No Dependencies**: Pure HTML/CSS/JavaScript - no build process required

## 📋 Word Categories

The game includes words from various categories:
- **Nouns**: Places, people, objects, animals, food, etc.
- **Verbs**: Action words across different tenses
- **Adjectives**: Descriptive words
- **Proper Nouns**: Famous people, places, brands, landmarks
- **Cultural References**: French culture, history, geography

## 🚀 Getting Started

### Option 1: Direct Use
Simply open `index.html` in your web browser. The game will automatically load the word list from the GitHub repository.

### Option 2: Local Development
1. Clone or download this repository
2. Open `index.html` in your web browser
3. The game will fetch the word list from the remote CSV file

### Option 3: Self-Hosted
1. Clone this repository
2. Serve the files using any web server (e.g., Python's `http.server`, Node.js `http-server`, or any web hosting service)
3. The game will work offline if you modify the `REMOTE_URL` in the code to point to a local file

## 📁 Project Structure

```
french-taboo/
├── index.html          # Main game file (HTML, CSS, JavaScript)
├── word-list.csv       # Word database with target words and taboo words
└── README.md          # This file
```

## 🎯 Game Rules

- **Objective**: Describe the target word without using any taboo words
- **Time Limit**: 60 seconds per round
- **Scoring**: 1 point per correctly guessed word
- **Skips**: 1 skip per round
- **Buzzer**: Use when a taboo word is mentioned or time expires
- **Level Selection**: Words are filtered by selected level (includes all lower levels)

## 🛠️ Technical Details

- **Frontend**: Pure HTML5, CSS3, JavaScript (ES6+)
- **Styling**: Tailwind CSS (via CDN)
- **Fonts**: Google Fonts (Lexend)
- **Data Source**: CSV file hosted on GitHub
- **Audio**: Web Audio API for buzzer sound
- **Storage**: Session-based (no persistent storage)

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
