<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Age Calculator</title>
    <!-- Load Tailwind CSS via CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styling for a vibrant, fun look */
        @import url('https://fonts.googleapis.com/css2?family=Chakra+Petch:wght@600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
            background: linear-gradient(145deg, #1f2937, #374151); /* Dark gradient background */
        }
        .trick-header {
            font-family: 'Chakra Petch', sans-serif;
            text-shadow: 0 0 10px rgba(74, 20, 140, 0.8); /* Purple glow */
        }
        .result-display {
            font-family: 'Chakra Petch', sans-serif;
            background: linear-gradient(90deg, #d8b4fe, #a78bfa); /* Light purple gradient */
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            font-size: 4rem; /* Base size */
        }
        @media (min-width: 640px) {
            .result-display {
                font-size: 6rem; /* Larger size on desktop */
            }
        }
    </style>
</head>
<body class="min-h-screen flex items-center justify-center p-6">

    <div class="w-full max-w-lg bg-gray-800 p-8 sm:p-10 rounded-2xl shadow-2xl border-t-4 border-purple-500">
        
        <h1 class="text-4xl sm:text-5xl font-extrabold text-purple-400 mb-2 trick-header">
            Simple Age Calculator
        </h1>
        <p class="text-gray-400 mb-8">
            Find out your age instantly! (Current Year: <span id="currentYearDisplay"></span>)
        </p>

        <!-- Input and Button -->
        <div class="space-y-4 mb-8">
            <label for="birthYear" class="block text-lg font-medium text-gray-300">
                What year were you born?
            </label>
            <input 
                type="number" 
                id="birthYear" 
                placeholder="e.g., 1995" 
                min="1900" 
                max="2025" 
                class="w-full p-3 border-2 border-purple-600 rounded-lg bg-gray-700 text-white placeholder-gray-500 focus:ring-purple-500 focus:border-purple-500 transition duration-150"
            >
            <button 
                id="calculateBtn" 
                class="w-full py-3 px-4 bg-purple-600 hover:bg-purple-700 text-white font-bold rounded-lg shadow-lg transition duration-200 transform hover:scale-[1.01] active:scale-100"
            >
                Calculate Age
            </button>
        </div>

        <!-- Result Display Area -->
        <div id="resultContainer" class="hidden text-center mt-8 p-6 bg-gray-700 rounded-xl border border-purple-600">
            <p class="text-xl font-medium text-gray-300 mb-4">Your Calculated Age is:</p>
            <div id="resultNumber" class="result-display font-black leading-none">
                <!-- Result will be displayed here -->
            </div>
            <p id="resultExplanation" class="text-gray-400 mt-4 text-sm sm:text-base">
                <!-- Explanation will be displayed here -->
            </p>
        </div>
        
        <!-- Error Message -->
        <div id="errorMsg" class="hidden mt-4 p-3 bg-red-800 text-white rounded-lg text-center">
            Please enter a valid birth year (4 digits, must be 2025 or earlier).
        </div>

    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // NOTE: We assume the current year is 2025 for this calculation, as it's the simplest way 
            // to show the direct math without dealing with specific birth months.
            const currentYear = new Date().getFullYear();
            
            // Display the current year in the heading
            document.getElementById('currentYearDisplay').textContent = currentYear;

            const birthYearInput = document.getElementById('birthYear');
            const calculateBtn = document.getElementById('calculateBtn');
            const resultContainer = document.getElementById('resultContainer');
            const resultNumber = document.getElementById('resultNumber');
            const resultExplanation = document.getElementById('resultExplanation');
            const errorMsg = document.getElementById('errorMsg');

            calculateBtn.addEventListener('click', calculateAge);

            function calculateAge() {
                const birthYear = parseInt(birthYearInput.value);

                // Validation
                if (isNaN(birthYear) || birthYear < 1900 || birthYear > currentYear) {
                    errorMsg.classList.remove('hidden');
                    resultContainer.classList.add('hidden');
                    return;
                }

                // Hide error message on successful input
                errorMsg.classList.add('hidden');

                // The New Formula: Current Year - Birth Year
                const age = currentYear - birthYear;

                // Display the results
                resultNumber.textContent = age;
                resultContainer.classList.remove('hidden');

                // Provide the explanation
                resultExplanation.innerHTML = `
                    The calculation performed is: ${currentYear} (Current Year) - ${birthYear} (Birth Year) = <span class="font-bold text-purple-300">${age}</span>.
                `;

                // Clear input after calculation for next guess
                birthYearInput.value = '';
            }
        });
    </script>
</body>
</html>

