# firebase-meme-guessing-game

# 🎭 Firebase Meme Guessing Game

A fun, interactive web application where users can guess what's happening in memes! Built with vanilla JavaScript and Firebase for real-time cloud storage.

## ✨ Features

- 🎮 **Interactive Gameplay** - Guess what's happening in hilarious memes
- 🔥 **Firebase Integration** - Real-time cloud storage with Firestore
- 🛡️ **Anti-Spam Protection** - Comprehensive security rules and content filtering
- 📱 **Responsive Design** - Works perfectly on desktop, tablet, and mobile
- ⌨️ **Keyboard Shortcuts** - Enhanced UX with keyboard navigation
- 🎨 **Modern UI** - Glassmorphism design with smooth animations
- 🔄 **Auto-Progression** - Automatically loads new memes after guessing
- 💾 **Offline Fallback** - Works locally if Firebase is unavailable
- 🚫 **Content Safety** - Built-in profanity filtering

## 🚀 Live Demo

**GitHub Pages:** [https://ananya-aidev.github.io/firebase-guessing-game/](https://ananya-aidev.github.io/firebase-guessing-game/)

## 🛠️ Technologies Used

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **Backend:** Firebase Firestore (NoSQL Database)
- **Security:** Firebase Security Rules
- **Styling:** Custom CSS with Glassmorphism, Poppins Font
- **Deployment:** GitHub Pages
- **Version Control:** Git & GitHub

## 📦 Installation & Setup

### Prerequisites
- A modern web browser
- Firebase account (free)
- GitHub account (for deployment)

### 1. Clone the Repository
```bash
git clone https://github.com/yourusername/firebase-meme-guessing-game.git
cd firebase-meme-guessing-game
```

### 2. Firebase Setup
1. Go to [Firebase Console](https://console.firebase.google.com)
2. Click "Create a project" or use existing project
3. Enable Firestore Database
4. Copy your Firebase configuration

### 3. Configure Firebase
Replace the Firebase config in `index.html` with your project credentials:
```javascript
const firebaseConfig = {
    apiKey: "your-api-key-here",
    authDomain: "your-project.firebaseapp.com",
    projectId: "your-project-id",
    storageBucket: "your-project.firebasestorage.app",
    messagingSenderId: "123456789",
    appId: "your-app-id"
};
```

### 4. Setup Security Rules
1. Go to Firebase Console → Firestore → Rules
2. Replace with these security rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /guesses/{guessId} {
      // Anyone can read
      allow read: if true;
      
      // Allow writes with basic validation
      allow create: if 
        // Required fields exist
        request.resource.data.keys().hasAll(['imageUrl', 'guess', 'timestamp']) &&
        
        // Data types are correct
        request.resource.data.imageUrl is string &&
        request.resource.data.guess is string &&
        request.resource.data.timestamp is timestamp &&
        
        // Length limits
        request.resource.data.guess.size() >= 3 &&
        request.resource.data.guess.size() <= 500 &&
        request.resource.data.imageUrl.size() <= 2048 &&
        
        // Basic spam protection
        !request.resource.data.guess.lower().matches('.*spam.*') &&
        !request.resource.data.guess.matches('^[0-9]+$') &&
        
        // Image URL must be HTTPS
        request.resource.data.imageUrl.matches('https://.*');
      
      // No updates or deletes
      allow update, delete: if false;
    }
    
    // Block everything else
    match /{document=**} {
      allow read, write: if false;
    }
  }
}
```

3. Click "Publish"

### 5. Test Locally
Open `index.html` in your browser or use a local server:
```bash
# Option 1: Simple Python server
python -m http.server 8000

# Option 2: Node.js server (if you have Node.js)
npx serve .

# Option 3: VS Code Live Server extension
```

## 🌐 Deployment

### GitHub Pages Deployment
1. Push your code to GitHub:
```bash
git add .
git commit -m "feat: Add Firebase-powered meme guessing game with real-time cloud storage

- Complete responsive web app with meme display and user guessing
- Firebase Firestore integration for real-time data persistence  
- Anti-spam security rules and content validation
- Progressive enhancement with offline fallback
- Mobile-optimized design with modern UI/UX
- Keyboard shortcuts and auto-progression features"

git push origin main
```

2. Enable GitHub Pages:
   - Go to repository Settings
   - Scroll to "Pages" section
   - Select "Deploy from a branch"
   - Choose "main" branch
   - Select "/ (root)" folder
   - Click "Save"

3. Your site will be live at: `https://yourusername.github.io/firebase-meme-guessing-game/`

## 🎮 How to Play

1. **View the Meme** - A random meme will be displayed
2. **Make Your Guess** - Type what you think is happening in the text field
3. **Submit** - Click "Submit Guess" or press Enter
4. **New Meme** - Click "New Meme" or use Ctrl/Cmd + N for a fresh challenge
5. **View All Guesses** - Scroll down to see what others have guessed

## ⌨️ Keyboard Shortcuts

- **Enter** - Submit your guess
- **Ctrl/Cmd + N** - Load new meme
- **Escape** - Focus input field

## 🛡️ Security Features

- **Input Validation** - Enforces minimum/maximum guess length
- **Anti-Spam Rules** - Blocks spam content and repeated characters
- **Content Filtering** - Built-in profanity filter
- **HTTPS Only** - Only accepts secure image URLs
- **No Data Modification** - Users cannot edit or delete existing guesses
- **Collection Protection** - Only allows access to guesses collection

## 📁 Project Structure

```
firebase-meme-guessing-game/
├── index.html              # Main application file
├── README.md              # Project documentation
├── security-rules.txt     # Firebase security rules
└── screenshots/           # App screenshots (optional)
    ├── desktop-view.png
    ├── mobile-view.png
    └── gameplay.gif
```

## 🎯 Learning Objectives

This project demonstrates:
- **Firebase Integration** - Firestore database setup and usage
- **Security Rules** - Database access control and validation
- **Real-time Data** - Live updates across multiple users
- **Responsive Design** - Mobile-first CSS approach
- **Error Handling** - Graceful fallbacks and user feedback
- **Modern JavaScript** - ES6+ features and async/await
- **UX Design** - Loading states, animations, and accessibility

## 🤝 Contributing

This is a learning project, but contributions are welcome!

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'feat: Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

## 🔗 Links

- **Live Demo:** [GitHub Pages Link](https://ananya-aidev.github.io/firebase-guessing-game/)




⭐ **Star this repository if you found it helpful!**

Built with ❤️ using Firebase and vanilla JavaScript
