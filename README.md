# Real-Time-Weather
This project is a weather forecast web application that uses the WEATHER API to retrieve weather data of most cities around the world and present it to the user in response to their specific entry.

```
document.addEventListener('DOMContentLoaded', function () {
    const tour = new Shepherd.Tour({
        defaultStepOptions: {
            cancelIcon: {
                enabled: true
            },
            classes: 'class-1 class-2',
            scrollTo: { behavior: 'smooth', block: 'center' }
        }
    });

    tour.addStep({
        title: 'Weather Search',
        text: 'Enter a city name and click the search button to get the current weather.',
        attachTo: {
            element: '.search-bar',
            on: 'bottom'
        },
        buttons: [
            {
                action() {
                    return this.next();
                },
                text: 'Next'
            }
        ]
    });

    tour.addStep({
        title: 'Weather Information',
        text: 'Here you will see the weather information for the searched city.',
        attachTo: {
            element: '.weather',
            on: 'top'
        },
        buttons: [
            {
                action() {
                    return this.back();
                },
                classes: 'shepherd-button-secondary',
                text: 'Back'
            },
            {
                action() {
                    return this.next();
                },
                text: 'Next'
            }
        ]
    });

    tour.addStep({
        title: 'GitHub Link',
        text: 'You can visit my GitHub profile by clicking this link.',
        attachTo: {
            element: 'a[target="_blank"]',
            on: 'top'
        },
        buttons: [
            {
                action() {
                    return this.back();
                },
                classes: 'shepherd-button-secondary',
                text: 'Back'
            },
            {
                action() {
                    return this.next();
                },
                text: 'Done'
            }
        ]
    });

    tour.start();
});
```

![image](https://github.com/kaiesamurai/Real-world-weather-app-shepardjs-quest-12/assets/168727731/47beaaad-3866-40c2-a5c7-fe07010f8201)
