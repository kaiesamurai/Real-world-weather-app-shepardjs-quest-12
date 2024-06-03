## Real-Time Weather Application

This project is a weather forecast web application that utilizes the WEATHER API to retrieve weather data for cities around the world and present it to the user based on their specific query. The project also incorporates Shepherd.js to provide a guided tour of the application's features.

### Features

- Retrieve and display current weather data for any city.
- User-friendly interface for entering city names.
- Detailed weather information including temperature, humidity, wind speed, and more.
- Interactive guided tour using Shepherd.js.

### Getting Started

#### Prerequisites

Before you begin, ensure you have met the following requirements:

- You have a modern web browser.
- You have an active internet connection.
- You have an API key from the WEATHER API provider.

#### Installation

1. Clone the repository:

    ```sh
    git clone https://github.com/yourusername/real-time-weather.git
    ```

2. Navigate to the project directory:

    ```sh
    cd real-time-weather
    ```

3. Open `index.html` in your favorite code editor and replace `YOUR_API_KEY_HERE` with your actual WEATHER API key.

### Usage

1. Open `index.html` in a web browser.

2. Enter the name of the city you want to get the weather information for in the search bar.

3. Click the "Get Weather" button to retrieve and display the weather data.

### Guided Tour

The application includes a guided tour using Shepherd.js to help users understand the different features of the application.

#### Starting the Tour

1. Open the application in your web browser.
2. Click the "Start Tour" button to initiate the Shepherd.js guided tour.
3. Follow the instructions provided by the tour to explore the features of the application.

### Code Structure

#### HTML (index.html)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Real-Time Weather</title>
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/shepherd.js/8.1.0/css/shepherd.css" />
    <script type="module" src="https://cdnjs.cloudflare.com/ajax/libs/shepherd.js/8.1.0/shepherd.esm.min.js"></script>
</head>
<body>
    <div id="app">
        <h1>Real-Time Weather</h1>
        <input type="text" id="cityInput" placeholder="Enter city name">
        <button id="getWeatherBtn">Get Weather</button>
        <button id="startTourBtn">Start Tour</button>
        <div id="weatherInfo"></div>
    </div>
    <script src="script.js"></script>
</body>
</html>
```

#### CSS (style.css)

```css
body {
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f0f0f0;
    margin: 0;
    padding: 0;
}

#app {
    margin: 50px auto;
    width: 300px;
    padding: 20px;
    background-color: white;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

input, button {
    width: 100%;
    padding: 10px;
    margin: 5px 0;
    border: 1px solid #ddd;
    border-radius: 5px;
}

button {
    background-color: #007BFF;
    color: white;
    cursor: pointer;
}

button:hover {
    background-color: #0056b3;
}

#weatherInfo {
    margin-top: 20px;
    text-align: left;
}
```

#### JavaScript (script.js)

```javascript
document.addEventListener('DOMContentLoaded', () => {
    const apiKey = 'YOUR_API_KEY_HERE';
    const cityInput = document.querySelector('#cityInput');
    const getWeatherBtn = document.querySelector('#getWeatherBtn');
    const weatherInfo = document.querySelector('#weatherInfo');
    const startTourBtn = document.querySelector('#startTourBtn');

    getWeatherBtn.addEventListener('click', getWeather);
    startTourBtn.addEventListener('click', startTour);

    function getWeather() {
        const city = cityInput.value;
        if (!city) {
            alert('Please enter a city name');
            return;
        }

        fetch(`https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${city}`)
            .then(response => response.json())
            .then(data => {
                if (data.error) {
                    weatherInfo.innerHTML = `<p>${data.error.message}</p>`;
                } else {
                    weatherInfo.innerHTML = `
                        <h2>${data.location.name}, ${data.location.country}</h2>
                        <p>Temperature: ${data.current.temp_c}°C</p>
                        <p>Condition: ${data.current.condition.text}</p>
                        <p>Humidity: ${data.current.humidity}%</p>
                        <p>Wind: ${data.current.wind_kph} kph</p>
                    `;
                }
            })
            .catch(error => {
                weatherInfo.innerHTML = `<p>Error fetching weather data. Please try again later.</p>`;
            });
    }

    function startTour() {
        const tour = new Shepherd.Tour({
            useModalOverlay: true,
            defaultStepOptions: {
                cancelIcon: {
                    enabled: true
                },
                classes: 'shadow-md bg-purple-dark',
                scrollTo: { behavior: 'smooth', block: 'center' }
            }
        });

        tour.addStep({
            id: 'welcome',
            text: 'Welcome to the Real-Time Weather application!',
            buttons: [
                {
                    text: 'Next',
                    action: tour.next
                }
            ]
        });

        tour.addStep({
            id: 'input',
            text: 'Enter the name of the city here.',
            attachTo: {
                element: '#cityInput',
                on: 'bottom'
            },
            buttons: [
                {
                    text: 'Back',
                    action: tour.back
                },
                {
                    text: 'Next',
                    action: tour.next
                }
            ]
        });

        tour.addStep({
            id: 'get-weather',
            text: 'Click this button to get the weather information for the entered city.',
            attachTo: {
                element: '#getWeatherBtn',
                on: 'bottom'
            },
            buttons: [
                {
                    text: 'Back',
                    action: tour.back
                },
                {
                    text: 'Next',
                    action: tour.next
                }
            ]
        });

        tour.addStep({
            id: 'weather-info',
            text: 'The weather information will be displayed here.',
            attachTo: {
                element: '#weatherInfo',
                on: 'top'
            },
            buttons: [
                {
                    text: 'Back',
                    action: tour.back
                },
                {
                    text: 'Finish',
                    action: tour.complete
                }
            ]
        });

        tour.start();
    }
});
```

### API Reference

- **Weather API**: This project uses the [Weather API](https://www.weatherapi.com/) to fetch real-time weather data. You need to sign up for an API key to use the service.

### Contributing

If you want to contribute to this project, please follow these steps:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/your-feature`).
3. Make your changes and commit them (`git commit -m 'Add some feature'`).
4. Push to the branch (`git push origin feature/your-feature`).
5. Create a new Pull Request.

### License

This project is open-source and available under the [MIT License](LICENSE).

### Acknowledgements

- [Weather API](https://www.weatherapi.com/) for providing the weather data.
- [Shepherd.js](https://shepherdjs.dev/) for the guided tour functionality.

---

This README provides an overview of the Real-Time Weather application, instructions for getting started, and a guide on how to use the integrated Shepherd.js tour feature.

![image](https://github.com/kaiesamurai/Real-world-weather-app-shepardjs-quest-12/assets/168727731/47beaaad-3866-40c2-a5c7-fe07010f8201)
