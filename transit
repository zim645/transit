<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Victoria Falls Transit Planner</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body {
            font-family: 'Inter', sans-serif;
        }
        .card {
            background-color: white;
            border-radius: 0.75rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        .btn-primary {
            background-color: #4f46e5;
            color: white;
            transition: background-color 0.3s ease;
        }
        .btn-primary:hover {
            background-color: #4338ca;
        }
        /* Using a real, high-quality background image */
        .hero-background {
            background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)), url('https://images.unsplash.com/photo-1547471080-771cb5f6a0b3?q=80&w=2070&auto=format&fit=crop');
            background-size: cover;
            background-position: center;
        }
        .icon-btn {
            background: transparent;
            border: none;
            cursor: pointer;
        }
    </style>
</head>
<body class="bg-gray-100">

    <div id="app" class="min-h-screen flex flex-col items-center justify-center p-4 hero-background">
        <div class="w-full max-w-3xl mx-auto bg-white/90 backdrop-blur-sm rounded-2xl shadow-2xl p-6 md:p-10">
            <header class="text-center mb-8">
                <h1 class="text-3xl md:text-4xl font-bold text-gray-800">Victoria Falls Transit Planner</h1>
                <p class="text-gray-600 mt-2">Your simple guide to getting around in Vic Falls, Zimbabwe.</p>
            </header>

            <main>
                <div class="flex items-center justify-center gap-4 mb-6">
                    <!-- Start Location Group -->
                    <div class="flex-1">
                        <label for="startLocation" class="block text-sm font-medium text-gray-700 mb-1">Start Location</label>
                        <div class="flex items-center gap-2">
                           <select id="startLocation" class="w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
                                <!-- Options populated by JS -->
                           </select>
                           <button id="useCurrentLocation" title="Use my current location" class="p-2 rounded-full hover:bg-gray-200 transition-colors">
                                <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-gray-600"><path d="M12 2L7 7l5 5 5-5-5-5z"/><path d="M2 12l5 5 5-5-5-5-5 5z"/></svg>
                           </button>
                        </div>
                    </div>
                    
                    <!-- Swap Button -->
                    <div class="pt-6">
                        <button id="swapLocations" title="Swap locations" class="p-2 rounded-full hover:bg-gray-200 transition-colors">
                            <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-gray-600"><path d="M8 3L4 7l4 4"/><path d="M4 7h16"/><path d="M16 21l4-4-4-4"/><path d="M20 17H4"/></svg>
                        </button>
                    </div>

                    <!-- End Location Group -->
                    <div class="flex-1">
                        <label for="endLocation" class="block text-sm font-medium text-gray-700 mb-1">Destination</label>
                        <select id="endLocation" class="w-full p-3 border border-gray-300 rounded-lg shadow-sm focus:ring-indigo-500 focus:border-indigo-500">
                             <!-- Options populated by JS -->
                        </select>
                    </div>
                </div>

                <!-- Plan Trip Button -->
                <div class="text-center mb-8">
                    <button id="planTripBtn" class="w-full md:w-auto btn-primary font-bold py-3 px-8 rounded-lg shadow-lg transform hover:scale-105">
                        Plan My Trip
                    </button>
                </div>
                
                <!-- Results Section -->
                <div id="results" class="hidden">
                    <h2 class="text-2xl font-bold text-gray-800 text-center mb-6">Your Trip Options</h2>
                    <div id="results-container" class="grid grid-cols-1 md:grid-cols-2 gap-6">
                        <!-- Results will be injected here -->
                    </div>
                     <div id="message-area" class="hidden mt-4 text-center p-3 rounded-lg"></div>
                </div>
            </main>
        </div>
        <footer class="text-center text-white/80 mt-8 text-sm">
            <p>Built with ❤️ for Victoria Falls travelers.</p>
        </footer>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // --- Expanded Data Store ---
            const localTransportData = {
                "Victoria Falls Hotel": { arrival_time: "10 min", cost: "$5", icon: "🏨" },
                "Zambezi National Park": { arrival_time: "15 min", cost: "$5", icon: "🐘" },
                "Town Center": { arrival_time: "5 min", cost: "$3", icon: "🏙️" },
                "Victoria Falls Airport (VFA)": { arrival_time: "20 min", cost: "$10", icon: "✈️" },
                "Curio Market": { arrival_time: "7 min", cost: "$2", icon: "🛍️" },
                "The Lookout Cafe": { arrival_time: "12 min", cost: "$6", icon: "☕" },
                "Elephant's Walk Shopping Village": { arrival_time: "8 min", cost: "$4", icon: "🐘" },
                "Boma Dinner & Drum Show": { arrival_time: "18 min", cost: "$8", icon: "🥁" },
                "Victoria Falls Bridge": { arrival_time: "15 min", cost: "$7", icon: "🌉" }
            };

            // --- UI Elements ---
            const startLocationSelect = document.getElementById('startLocation');
            const endLocationSelect = document.getElementById('endLocation');
            const planTripBtn = document.getElementById('planTripBtn');
            const resultsDiv = document.getElementById('results');
            const resultsContainer = document.getElementById('results-container');
            const messageArea = document.getElementById('message-area');
            const useCurrentLocationBtn = document.getElementById('useCurrentLocation');
            const swapLocationsBtn = document.getElementById('swapLocations');

            // --- Functions ---
            
            function showMessage(text, type = 'error') {
                messageArea.textContent = text;
                messageArea.className = `mt-4 text-center p-3 rounded-lg ${type === 'error' ? 'bg-red-100 text-red-600' : 'bg-blue-100 text-blue-600'}`;
                messageArea.classList.remove('hidden');
                resultsDiv.classList.remove('hidden');
            }

            function populateLocations() {
                const locations = Object.keys(localTransportData);
                startLocationSelect.innerHTML = '';
                endLocationSelect.innerHTML = '';
                
                locations.forEach(location => {
                    const optionStart = document.createElement('option');
                    optionStart.value = location;
                    optionStart.textContent = location;
                    startLocationSelect.appendChild(optionStart);

                    const optionEnd = document.createElement('option');
                    optionEnd.value = location;
                    optionEnd.textContent = location;
                    endLocationSelect.appendChild(optionEnd);
                });
                if (locations.length > 1) {
                    endLocationSelect.selectedIndex = 1;
                }
            }
            
            function getLocalTaxiInfo(startLocation, endLocation) {
                const time = 10 + Math.floor(Math.random() * 8);
                const cost = 4 + Math.floor(Math.random() * 3);
                return { service: "Local Taxi", estimated_time: `${time} min`, cost: `$${cost}`, icon: "🚕" };
            }

            function planTrip() {
                const startLocation = startLocationSelect.value;
                const endLocation = endLocationSelect.value;

                resultsDiv.classList.add('hidden');
                messageArea.classList.add('hidden');
                resultsContainer.innerHTML = ''; 

                if (startLocation === endLocation) {
                    showMessage('Start and destination cannot be the same. Please choose a different destination.', 'error');
                    return;
                }

                const taxiInfo = getLocalTaxiInfo(startLocation, endLocation);
                const sharedTransportInfo = localTransportData[endLocation];

                displayResults(taxiInfo, sharedTransportInfo);
                resultsDiv.classList.remove('hidden');
            }
            
            function displayResults(taxi, shared) {
                 const taxiCard = `
                    <div class="card p-6 flex flex-col items-center text-center">
                        <div class="text-6xl mb-3">${taxi.icon}</div>
                        <h3 class="text-xl font-bold text-gray-800">${taxi.service}</h3>
                        <p class="text-gray-600 mt-2">A private and direct option, available on demand.</p>
                        <div class="mt-4 text-lg">
                            <span class="font-semibold text-indigo-600">${taxi.estimated_time}</span> | 
                            <span class="font-semibold text-green-600">${taxi.cost}</span>
                        </div>
                    </div>
                `;

                const sharedCard = `
                     <div class="card p-6 flex flex-col items-center text-center">
                        <div class="text-6xl mb-3">${shared.icon}</div>
                        <h3 class="text-xl font-bold text-gray-800">Local Shuttle</h3>
                        <p class="text-gray-600 mt-2">A shared, cost-effective option for this destination.</p>
                        <div class="mt-4 text-lg">
                            <span class="font-semibold text-indigo-600">${shared.arrival_time}</span> | 
                            <span class="font-semibold text-green-600">${shared.cost}</span>
                        </div>
                    </div>
                `;
                
                resultsContainer.innerHTML = taxiCard + sharedCard;
            }

            function handleCurrentLocation() {
                if (!navigator.geolocation) {
                    showMessage('Geolocation is not supported by your browser.', 'error');
                    return;
                }

                showMessage('Getting your location...', 'info');

                navigator.geolocation.getCurrentPosition(
                    (position) => {
                        messageArea.classList.add('hidden');
                        // For this app, we don't need the exact coords, just to indicate we're using them.
                        // We will add a temporary option to the dropdown.
                        if (!startLocationSelect.querySelector('option[value="Current Location"]')) {
                            const currentLocOption = document.createElement('option');
                            currentLocOption.value = "Current Location";
                            currentLocOption.textContent = "📍 My Current Location";
                            startLocationSelect.prepend(currentLocOption);
                        }
                        startLocationSelect.value = "Current Location";
                    },
                    () => {
                        showMessage('Unable to retrieve your location. Please select one manually.', 'error');
                    }
                );
            }
            
            function handleSwapLocations() {
                const startIndex = startLocationSelect.selectedIndex;
                const endIndex = endLocationSelect.selectedIndex;
                startLocationSelect.selectedIndex = endIndex;
                endLocationSelect.selectedIndex = startIndex;
            }

            // --- Event Listeners ---
            planTripBtn.addEventListener('click', planTrip);
            useCurrentLocationBtn.addEventListener('click', handleCurrentLocation);
            swapLocationsBtn.addEventListener('click', handleSwapLocations);

            // --- Initial Setup ---
            populateLocations();
        });
    </script>
</body>
</html>
