# my-notes
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Languages</title> <!-- Updated title -->
    <style>
        body {
            background-color: #121212; /* Dark background */
            color: white; /* White text */
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 50px;
            position: relative;
            overflow: hidden; /* Prevent overflow from emojis */
        }

        button {
            padding: 15px 30px;
            font-size: 20px;
            cursor: pointer;
            background-color: #ffffff; /* White button */
            color: #121212; /* Dark text */
            border: none;
            border-radius: 5px;
            transition: background-color 0.3s;
            position: relative; /* Ensure button is above emojis */
            z-index: 2; /* Higher z-index for the button */
        }

        button:hover {
            background-color: #e0e0e0; /* Light gray on hover */
        }

        .emoji {
            position: absolute;
            font-size: 50px; /* Emoji size */
            pointer-events: auto; /* Allow clicks on emojis */
            z-index: 1; /* Lower z-index for emojis */
        }

        /* Define keyframe animations */
        @keyframes flyOut {
            0% { transform: translateY(0); }
            100% { transform: translateY(-200px) translateX(100px); opacity: 0; }
        }

        @keyframes jiggle {
            0%, 100% { transform: rotate(0deg); }
            25% { transform: rotate(15deg); }
            50% { transform: rotate(-15deg); }
            75% { transform: rotate(10deg); }
        }

        @keyframes breakEffect {
            0% { transform: scale(1); }
            50% { transform: scale(1.2); opacity: 0.7; }
            100% { transform: scale(0); opacity: 0; }
        }

        #finalMessage {
            display: none; /* Hidden by default */
            font-size: 30px; /* Message size */
            margin-top: 20px; /* Space above the message */
            opacity: 0; /* Start hidden */
            animation: fadeInBounce 1s forwards; /* Fade-in and bounce animation */
            z-index: 2; /* Higher z-index for the final message */
        }

        /* Fade-in and bounce animation */
        @keyframes fadeInBounce {
            0% {
                opacity: 0;
                transform: translateY(20px);
            }
            60% {
                opacity: 1;
                transform: translateY(-10px);
            }
            100% {
                transform: translateY(0);
            }
        }

        /* Style for date and time */
        #date {
            position: absolute; /* Absolute positioning */
            top: 20px; /* Distance from the top */
            left: 20px; /* Distance from the left */
            font-size: 20px; /* Font size */
            color: #e0e0e0; /* Light gray text */
            z-index: 3; /* Higher z-index for date */
        }

        #time {
            position: absolute; /* Absolute positioning */
            top: 50px; /* Distance from the top (below the date) */
            left: 20px; /* Distance from the left */
            font-size: 20px; /* Font size */
            color: #e0e0e0; /* Light gray text */
            z-index: 3; /* Higher z-index for time */
        }

    </style>
</head>
<body>
    <h1>Languages</h1> <!-- Updated title in the body -->
    <div id="date"></div> <!-- Date display -->
    <div id="time"></div> <!-- Time display -->
    <button id="openPdfButton">css&java</button>
    <div id="finalMessage">time to lock in</div> <!-- Final message -->

    <script>
        // Function to open the PDF
        document.getElementById('openPdfButton').addEventListener('click', function() {
            window.open('https://supersimpledev.github.io/references/html-css-reference.pdf', '_blank');
        });

        // Function to generate random emojis
        function createRandomEmojis() {
            const emojis = ['😊', '🎉', '🚀', '🌟', '✨', '💖', '🎈', '🌈', '💫', '🌻'];
            const numberOfEmojis = 30; // Number of emojis to generate

            for (let i = 0; i < numberOfEmojis; i++) {
                const emoji = document.createElement('div');
                emoji.className = 'emoji';
                emoji.innerText = emojis[Math.floor(Math.random() * emojis.length)];

                // Randomize position
                emoji.style.top = Math.random() * 70 + 20 + 'vh'; // Random vertical position below the header
                emoji.style.left = Math.random() * 100 + 'vw'; // Random horizontal position
                document.body.appendChild(emoji);

                // Add click event to make the emoji animate
                emoji.addEventListener('click', () => {
                    // Choose a random animation effect
                    const animationType = Math.floor(Math.random() * 3); // 0-2 for three effects

                    if (animationType === 0) {
                        emoji.style.animation = 'flyOut 0.5s forwards'; // Fly out animation
                    } else if (animationType === 1) {
                        emoji.style.animation = 'jiggle 0.5s forwards'; // Jiggle animation
                    } else {
                        emoji.style.animation = 'breakEffect 0.5s forwards'; // Break effect animation
                    }

                    // Remove the emoji from the DOM after animation to prevent multiple clicks
                    setTimeout(() => {
                        emoji.remove();
                        checkForEmojis(); // Check if any emojis are left
                    }, 500); // Match timeout with the animation duration
                });
            }
        }

        // Function to check for remaining emojis and display the final message
        function checkForEmojis() {
            const emojis = document.querySelectorAll('.emoji');
            if (emojis.length === 0) {
                document.getElementById('finalMessage').style.display = 'block'; // Show the final message
            }
        }

        // Function to display the current date
        function displayDate() {
            const dateElement = document.getElementById('date');
            const options = { year: 'numeric', month: 'long', day: 'numeric', weekday: 'long' };
            const currentDate = new Date().toLocaleDateString('en-US', options);
            dateElement.innerText = `Today is ${currentDate}`;
        }

        // Function to display the current time
        function displayTime() {
            const timeElement = document.getElementById('time');
            setInterval(() => {
                const now = new Date();
                const hours = String(now.getHours()).padStart(2, '0'); // Format hours
                const minutes = String(now.getMinutes()).padStart(2, '0'); // Format minutes
                const seconds = String(now.getSeconds()).padStart(2, '0'); // Format seconds
                timeElement.innerText = `Current Time: ${hours}:${minutes}:${seconds}`;
            }, 1000); // Update every second
        }

        // Call the functions
        createRandomEmojis();
        displayDate();
        displayTime();
    </script>
</body>
</html>
