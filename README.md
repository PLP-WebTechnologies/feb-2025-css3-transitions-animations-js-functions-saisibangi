<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Button Animation with localStorage</title>
    <style>
        /* CSS Animation */
        .animated-button {
            padding: 12px 24px;
            font-size: 16px;
            cursor: pointer;
            border: none;
            background-color: #4CAF50;
            color: white;
            border-radius: 4px;
            transition: all 0.3s ease;
        }
        /* Animation keyframes */
        @keyframes scaleRotate {
            0% {
                transform: scale(1) rotate(0deg);
            }
            50% {
                transform: scale(1.2) rotate(180deg);
            }
            100% {
                transform: scale(1) rotate(360deg);
            }
        }
        /* Animation class */
        .animate {
            animation: scaleRotate 0.6s ease-in-out;
        }
        /* Preference toggle styling */
        .preference-container {
            margin: 20px;
        }
        label {
            margin-right: 10px;
        }
    </style>
</head>
<body>
    <div class="preference-container">
        <label for="animationToggle">Enable Animation:</label>
        <input type="checkbox" id="animationToggle" checked>
    </div>
    <button class="animated-button" id="actionButton">Click Me!</button>
    <script>
        // JavaScript to handle animation and localStorage
        (function () {
            // Elements
            const button = document.getElementById('actionButton');
            const toggle = document.getElementById('animationToggle');
            // Function to save preference to localStorage
            function savePreference() {
                localStorage.setItem('animationEnabled', toggle.checked);
            }
            // Function to load preference from localStorage
            function loadPreference() {
                const isEnabled = localStorage.getItem('animationEnabled');
                toggle.checked = isEnabled !== 'false'; // Default to true if not set
            }
            // Function to trigger animation
            function triggerAnimation() {
                if (toggle.checked) {
                    button.classList.add('animate');
                    // Remove animation class after animation completes
                    setTimeout(() => {
                        button.classList.remove('animate');
                    }, 600); // Matches animation duration
                }
            }
            // Initialize preference
            loadPreference();
            // Event listeners
            button.addEventListener('click', triggerAnimation);
            toggle.addEventListener('change', savePreference);
        })();
    </script>
</body>
</html>
