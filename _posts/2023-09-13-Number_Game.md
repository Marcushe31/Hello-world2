---
comments: true
layout: post
title: Number Game
type: hacks
courses: {'compsci': {'week': 4}}
categories: ['C4.1']
---
<html>
<head>
    <title>Number Guessing Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
        }
        #output {
            font-size: 24px;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Number Guessing Game</h1>
    <p>Guess a number between 1 and 20:</p>
    <input type="number" id="guess" min="1" max="20">
    <button onclick="checkGuess()">Submit Guess</button>
    <p id="output"></p>
    <!-- Add an image element with the src attribute pointing to your image file -->
    <img id="winnerImage" style="display: none;" src="https://www.goodfreephotos.com/albums/art-and-illustrations/emotiguy-thumbs-up-guy.png" alt="Thumbs Up Image">
    <!-- Add a button to restart the game -->
    <button id="restartButton" style="display: none;" onclick="restartGame()">Restart Game</button>
    <script>
        let randomNumber;
        let attempts = 0;
        function startGame() {
            // Generate a random number between 1 and 20
            randomNumber = Math.floor(Math.random() * 20) + 1;
            attempts = 0;
            // Clear the input field and output
            document.getElementById("guess").value = "";
            document.getElementById("output").innerHTML = "";
            document.getElementById("output").style.color = "";
            document.getElementById("guess").disabled = false;
            // Hide the image and restart button
            document.getElementById("winnerImage").style.display = "none";
            document.getElementById("restartButton").style.display = "none";
        }
        function checkGuess() {
            const guess = parseInt(document.getElementById("guess").value);
            attempts++;
            const output = document.getElementById("output");
            const winnerImage = document.getElementById("winnerImage");
            const restartButton = document.getElementById("restartButton");
            if (guess === randomNumber) {
                output.innerHTML = `Congratulations! You guessed the number ${randomNumber} in ${attempts} attempts.`;
                output.style.color = "green";
                document.getElementById("guess").disabled = true;
                // Display the image when the user guesses correctly
                winnerImage.style.display = "block";
                // Display the restart button
                restartButton.style.display = "block";
            } else if (guess < randomNumber) {
                output.innerHTML = "Try a higher number.";
                output.style.color = "red";
            } else {
                output.innerHTML = "Try a lower number.";
                output.style.color = "red";
            }
        }
        function restartGame() {
            // Reset the game
            startGame();
        }
        // Start the game when the page loads
        startGame();
    </script>
</body>
</html>
