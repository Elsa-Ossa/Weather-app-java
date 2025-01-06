# Weather Dashboard Application

A lightweight and user-friendly web application that allows users to search for current weather information by entering a city name. The app fetches real-time weather data using the OpenWeatherMap API and displays details such as temperature, humidity, weather condition, and an icon representing the weather.

---

## Features
- Search weather by city name.
- Displays:
  - Current temperature (°C).
  - Humidity level (%).
  - Weather condition (e.g., sunny, cloudy, rainy).
  - Weather icon.
- Real-time data fetched from OpenWeatherMap.
- Basic error handling for invalid cities or empty input.
- Loading indicator while fetching data.
- Responsive design for better usability across devices.

---

## Technologies Used
- **HTML**: Structure of the application.
- **CSS**: Styling and layout design.
- **JavaScript**: Dynamic behavior and API integration.
- **OpenWeatherMap API**: For fetching weather data.

---

## Setup Instructions

###1. Clone the Repository
```bash
git clone https://github.com/yourusername/weather-app.git
cd weather-app
2. Install a Live Server
Ensure you have a local server to run the app. If using Visual Studio Code, install the Live Server Extension.

3. Get a Free API Key
Sign up at OpenWeatherMap to get your free API key.
Replace 'YOUR_API_KEY' in the script.js file with your actual API key:
javascript
Copy code
const apiKey = 'your_actual_api_key';
4. Run the Application
Open index.html in Visual Studio Code.
Right-click the file and select "Open with Live Server".
The app will open in your default browser.
Usage
Enter the name of a city in the input field.
Click the Search button.
View the weather details in the display area:
Temperature.
Humidity.
Weather condition.
Weather icon.
If the city is invalid, you'll see an error message.
File Structure
bash
Code
weather-app/
│
├── index.html        # HTML structure of the app
 <!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather Dashboard</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div id="app">
        <h1>Weather Dashboard</h1>
        <input type="text" id="cityInput" placeholder="Enter city name">
        <button id="searchButton">Search</button>
        <div id="loading" style="display: none;">Loading...</div>
        <div id="weatherDisplay"></div>
    </div>
    <script src="script.js" defer></script>
</body>
</html>

├── style.css         # CSS styling for the app
 /* General Styles */
body {
    font-family: Arial, sans-serif;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #f0f0f0;
    margin: 0;
}

/* Application Container */
#app {
    text-align: center;
    background: white;
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

/* Input Field */
#cityInput {
    padding: 10px;
    width: 250px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
}

/* Search Button */
#searchButton {
    padding: 10px 20px;
    cursor: pointer;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 5px;
    font-size: 16px;
}

#searchButton:hover {
    background-color: #0056b3;
}

/* Weather Display */
#weatherDisplay img {
    width: 50px;
    height: 50px;
}

#loading {
    font-size: 16px;
    color: #555;
}

/* Responsive Design */
@media (max-width: 600px) {
    #cityInput {
        width: 100%;
    }

    #app {
        width: 90%;
    }
}


├── script.js         # JavaScript for API calls and dynamic behavior
                      // Add event listener to the Search button
document.getElementById('searchButton').addEventListener('click', fetchWeather);

// Fetch Weather Function
async function fetchWeather() {
    const city = document.getElementById('cityInput').value;
    const apiKey = 'YOUR_API_KEY'; // Replace with your OpenWeatherMap API key
    const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;
    const loading = document.getElementById('loading');
    const weatherDisplay = document.getElementById('weatherDisplay');

    // Clear previous data and show loading indicator
    weatherDisplay.innerHTML = '';
    loading.style.display = 'block';

    if (city.trim() === '') {
        weatherDisplay.innerHTML = '<p>Please enter a city name.</p>';
        loading.style.display = 'none';
        return;
    }

    try {
        const response = await fetch(url);
        if (!response.ok) {
            throw new Error('City not found');
        }

        const data = await response.json();
        displayWeather(data);
    } catch (error) {
        weatherDisplay.innerHTML = `<p>${error.message}</p>`;
    } finally {
        loading.style.display = 'none';
    }
}

// Display Weather Function
function displayWeather(data) {
    const weatherDisplay = document.getElementById('weatherDisplay');
    const temperature = data.main.temp;
    const humidity = data.main.humidity;
    const description = data.weather[0].description;
    const icon = `http://openweathermap.org/img/wn/${data.weather[0].icon}.png`;

    weatherDisplay.innerHTML = `
        <h2>Weather in ${data.name}</h2>
        <img src="${icon}" alt="${description}">
        <p>Temperature: ${temperature}°C</p>
        <p>Humidity: ${humidity}%</p>
        <p>Condition: ${description}</p>
    `;
}



└── README.md         # Project documentation


Screenshots
Weather Dashboard Interface



Improvements for Future Versions
Add 7-day weather forecast.
Include support for geolocation to detect user’s current location.
Allow users to save favorite cities for quick access.
Add unit conversion (Celsius to Fahrenheit).
License
This project is open-source and available under the MIT License.

Code:







