---
comments: true
layout: post
title: Hangman
type: hacks
courses: {'compsci': {'week': 4}}
categories: ['C4.1']
---

<html>
<head>
    <title>Hangman Game</title>
    <style>
    </style>
</head>
<body>
    <h1>Hangman Game</h1>
    <p>Guess the word:</p>
    <div id="word-container"></div>
    <p>Incorrect Guesses: <span id="incorrect-guesses">0</span></p>
    <p>Incorrect Letters: <span id="incorrect-letters"></span></p>
    <input type="text" id="guess-input" maxlength="1">
    <button onclick="makeGuess()">Guess</button>
    <button onclick="newGame()">New Game</button>
    <script>
        // Define an array of words for the game
        const words = ["apple", "banana", "cherry", "orange", "grape", "kiwi", "lemon", "monkey", "bird", "happy", " Pneumonoultramicroscopicsilicovolcanoconiosis", "mango"];
        let word; // The word to guess
        let guessedWord; // The word with guessed letters
        let incorrectGuesses = 0; // Number of incorrect guesses
        let incorrectLetters = []; // Incorrectly guessed letters
        const maxIncorrectGuesses = 6; // Maximum allowed incorrect guesses
        // Function to start a new game
        function newGame() {
            word = words[Math.floor(Math.random() * words.length)]; // Randomly select a word
            guessedWord = "_".repeat(word.length); // Initialize guessedWord with underscores
            incorrectGuesses = 0; // Reset incorrect guesses
            incorrectLetters = []; // Reset incorrect letters
            updateDisplay();
        }
        // Function to update the display
        function updateDisplay() {
            document.getElementById("word-container").textContent = guessedWord;
            document.getElementById("incorrect-guesses").textContent = incorrectGuesses;
            document.getElementById("incorrect-letters").textContent = incorrectLetters.join(", ");
        }
        // Function to make a guess
        function makeGuess() {
            const guess = document.getElementById("guess-input").value.toLowerCase();
            if (guess.length !== 1 || !guess.match(/[a-z]/)) {
                alert("Please enter a single letter.");
                return;
            }
            if (word.includes(guess)) {
                // Update guessedWord with correctly guessed letter(s)
                for (let i = 0; i < word.length; i++) {
                    if (word[i] === guess) {
                        guessedWord = guessedWord.substring(0, i) + guess + guessedWord.substring(i + 1);
                    }
                }
            } else {
                incorrectGuesses++;
                incorrectLetters.push(guess);
            }
            // Check if the game is won or lost
            if (guessedWord === word) {
                alert("Congratulations! You guessed the word: " + word);
                newGame();
            } else if (incorrectGuesses >= maxIncorrectGuesses) {
                alert("Game over. The word was: " + word);
                newGame();
            }
            // Clear the input field and update the display
            document.getElementById("guess-input").value = "";
            updateDisplay();
        }
        // Start a new game when the page loads
        window.onload = newGame;
    </script>
</body>
</html>
