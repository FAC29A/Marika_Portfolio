# Weeks 4 - 6
Learn how to manage asynchronous tasks and send HTTP requests using JavaScript. 
Examples are based on the project, [**Earth & Mars Weather App**](https://fac29a.github.io/Marika_Lucy_app/).

## 1. Write code that executes asynchronously
In our weather app project, fetch is used to get data from different APIs (Unsplash, NASA Mars, and weather API).
The code incorporates the use of `async` and `await` keywords, especially evident in the `fetchUnsplashImage()` function. This highlights the asynchronous nature of these operations. Specifically:
- The `fetchUnsplashImage()` function is defined using the `async` keyword.
- Within this function, the `await` keyword is employed during the `fetch()` call to the Unsplash API. This ensures that the function pauses and waits for the asynchronous fetch operation to finish before it progresses.

```js
async function fetchUnsplashImage() {
    const unsplashUrl = `https://api.unsplash.com/search/photos?query=someCity&orientation=landscape`;

    try {
        const response = await fetch(unsplashUrl, {
            headers: {
                Authorization: `Client-ID someAccessKey`,
            },
        });

        if (!response.ok) {
            throw new Error('Failed to fetch from Unsplash');
        }

        const data = await response.json();
        const imageUrl = data.results[0].urls.full; 
        
    } catch (error) {
        console.error('Error fetching image from Unsplash:', error);
    }
}

```



## 2. Use callbacks to access values that aren’t available synchronously
By nature, data fetched from an API isn't instantaneously available; it requires waiting for the server to process the request and respond. This is where callbacks — functions passed as arguments to other functions to be executed once the latter completes — become indispensable.

In our integration with the NASA Mars API for the project, we used callbacks to process the data only after it has been successfully retrieved. This ensured smooth, sequential execution and eliminated potential temporal discrepancies.


```js
// ================= NASA MARS API ================= 
document.getElementById('loadingIndicator').style.display = 'block';
nasaAPI
    .then((response) => response.json())
    .then((marsData) => {
        const solsArray = marsData.soles;
        solsArray.sort((a, b) => new Date(b.First_UTC) - new Date(a.First_UTC));

        // ... rest of the code

        });
```
By chaining `.then()` callbacks, we were able to first transform the raw response into a JSON format and subsequently process the Mars data.


## 3. Use promises to access values that aren’t available synchronously
I used `await Promise.all(promises)` to ensure that the code waits for all these asynchronous data fetching operations to finish before proceeding. This approach allows me to access values like user input and data fetched from remote sources, which may not be available synchronously, in a controlled and organised manner within the code.

```js
document.getElementById('loadingIndicator').style.display = 'flex';
    await new Promise(resolve => setTimeout(resolve, 1000));

    const cityInput = document.getElementById('earthCityInput');

    if (cityInputValue) {
        updateUserCity(cityInputValue);

        const promises = marsDates.map((marsDate, dayIndex) => fetchWeatherForCity(userCity, marsDate, dayIndex));
        await Promise.all(promises); // Wait for all fetches to complete

        // Stop the loading indicator after all fetches are done
        document.getElementById('loadingIndicator').style.display = 'none';
    }
```

## 4. Use the fetch method to make HTTP requests and receive responses

To fetch the weather data for a city, I used the following:


```js
// Function to fetch weather data for a specific city
async function getWeatherForCity(city) {
    try {
        const response = await fetch(`${apiUrl}?key=${apiKey}&q=${city}`);
        if (!response.ok) {
            throw new Error(`Failed to fetch weather data: ${response.statusText}`);
        }
        const weatherData = await response.json();
        console.log(`Weather data for ${city}:`, weatherData);
        return weatherData;
    } catch (error) {
        console.error('Error fetching weather data:', error);
        throw error;
    }
}
```

When the user wants to gather the current weather details for a specific location, we employ the `fetch` method to communicate with weather service providers. The `fetch` method allows our application to make asynchronous HTTP requests, meaning that while our application awaits data from the server, it remains responsive to user interactions. Once a request is sent, the server processes it and sends back an appropriate response, often in JSON format, which we then interpret and present to the user.

## 5. Configure the options argument of the fetch method to make GET and POST requests
When fetching images from Unsplash based on the user's city input or Mars, we perform a `GET` request. The Unsplash API requires an authorisation header for authentication. To cater to this, I configure the `fetch` method with an options argument that includes the necessary headers. These headers contain our access key which authenticates our application with the Unsplash service.

Similarly, for fetching weather data based on a given city and date, we perform a `GET` request. This request is formulated by constructing the URL using query parameters, which includes the API key, the city's name, and the date.

Here's a snippet from the code that illustrates these configurations:

```js
// Fetching an image from Unsplash for a given city
const response = await fetch(unsplashUrl, {
    headers: {
        Authorization: `Client-ID ${unsplashAccessKey}`,
    },
});

// Fetching weather data for a given city and date
const url = new URL(apiUrl);
url.search = new URLSearchParams(queryParams);
const response = await fetch(URL);
```


## 6. Use the map array method to create a new array containing new values
Upon obtaining the Mars weather data for recent sols (Martian days), I needed to reformat the terrestrial dates into a friendly, readable format. To achieve this, I used the `map` method to iterate over each sol's date, split it, and reassemble it in the desired format. Here's a snippet that demonstrates this:

```js
// Extract the terrestrial_date from the Mars API data
marsDates = last7Sols.map(sol => {
    const dateParts = sol.terrestrial_date.split('-'); // Split the date string
    const year = dateParts[0];
    const month = dateParts[1];
    const day = dateParts[2];

    // Define an array of month names
    const monthNames = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];

    // Reformat the date as 'DD Mon YYYY'
    return `${day} ${monthNames[parseInt(month, 10) - 1]} ${year}`;
});
console.log(marsDates);
```


## 7. Use the filter array method to create a new array with certain values removed

## 8. Access DOM nodes using a variety of selectors
I adopted the `querySelector` and `querySelectorAll` methods to select and manipulate specific elements in the DOM. Here's an example of how I used these methods to grab all the buttons with a class name of `filter-btn`:

```js
const buttons = document.querySelectorAll('.filter-btn');
```
To fetch a specific element, like the container responsible for displaying background images:

```js
const backgroundContainer = document.querySelector('.background-container');
```


## 9. Add and remove DOM nodes to change the content on the page


## 10. Toggle the classes applied to DOM nodes to change their CSS properties

```js
// Start the loading indicator
    document.getElementById('loadingIndicator').style.display = 'flex';


// Stop the loading indicator after all fetches are done
        document.getElementById('loadingIndicator').style.display = 'none';
```
 

We implemented a `loadingIndicator` function that dynamically toggles the classes applied to DOM nodes, resulting in changes to their CSS properties. This `loadingIndicator` becomes visible when a user enters a city name in the search bar. Its visibility is controlled by the toggling of CSS properties, providing users with a visual cue while data is being fetched. You can observe this functionality in action when the user clicks the 'Search' button.

<img width="1280" alt="Screenshot 2023-10-25 at 23 34 02" src="https://github.com/FAC29A/Marika_Portfolio/assets/126022615/5338ca2a-a4ce-44a1-8f6d-6e8cc3b1ccc1">

## 11. Use consistent layout and spacing
In this code snippet, we've demonstrated the consistent usage of padding, margins, and button colour schemes, while effectively applying colour contrasts to distinguish the header, content, and footer sections. This CSS code ensures a uniform layout and consistent spacing throughout the user interface. 

```js
/* Apply consistent padding and spacing for buttons */
.button {
    padding: 10px 20px;
    margin: 5px;
    background-color: #0074d9;
    color: #fff;
    border: none;
    border-radius: 5px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.button:hover {
    background-color: #0056a7;
}

/* Ensure color contrast to distinguish interface sections */
.header {
    background-color: #333;
    color: #fff;
    padding: 20px;
    text-align: center;
}

.content {
    background-color: #f2f2f2;
    padding: 20px;
    text-align: center;
}

.footer {
    background-color: #333;
    color: #fff;
    padding: 20px;
    text-align: center;
}

/* Maintain font consistency across sections */
.header,
.content,
.footer {
    font-family: Arial, sans-serif;
}
```

## 12. Follow a spacing guideline to give our app a consistent feel
I've consistently followed a spacing guideline to ensure our app maintains a cohesive and balanced appearance. 

<img width="978" alt="Screenshot 2023-10-25 at 23 27 32" src="https://github.com/FAC29A/Marika_Portfolio/assets/126022615/8fd32875-d966-4d19-836c-04eca280702b">







## 13. Debug client side JS in our web browser
Debugging is an essential part of ensuring our web application functions smoothly and without errors. In this code snippet, I've incorporated various debugging techniques to identify and address potential issues:

```js
// Fetches an image from Unsplash based on the user's city input.
const unsplashUrl = `https://api.unsplash.com/search/photos?query=${cityName}&orientation=landscape`;
    console.log('Requesting Unsplash URL:', unsplashUrl);

    try {
        const response = await fetch(unsplashUrl, {
            headers: {
                Authorization: `Client-ID ${unsplashAccessKey}`,
            },
        });

        // If the fetch isn't successful, retrieve a Mars image
        if (!response.ok) {
            // throw new Error(`Failed to fetch image from NASA ${response.status} ${response.statusText}`);
            await fetchMarsImage();
            return;
        }

        // ... (Code for processing and setting the fetched image)

    } catch (error) {
        console.error('Error fetching image from Unsplash:', error);
        await fetchMarsImage(); // When there's an error, fetch Mars image from Unsplash
    }
}

// ... (Other fetching functions)

// ================= NASA MARS API ================= 
document.getElementById('loadingIndicator').style.display = 'block';
nasaAPI
    .then((response) => response.json())
    .then((marsData) => {
        // ... (Code for processing Mars API data)

        // Populate the buttons with terrestrial dates
        buttons.forEach((button, index) => {
            button.textContent = marsDates[index];
            console.log("Mars Parameter Data:", parameterData.mars);
        });

        // ... (Rest of the code)

    })
    .catch((error) => console.log(error));
// Stop the loading indicator in case of error
document.getElementById('loadingIndicator').style.display = 'none';
```
In this code, I placed `console.log()` statements to log relevant information and data during various stages of execution. These log messages serve as invaluable tools for tracing the flow of the program, inspecting variable values, and detecting any errors that may occur.


## 14. Use console.log() to help us debug our code
We also used `console.log()` regularly to monitor and troubleshoot potential issues with the remote API servers. This helps us maintain the reliability and functionality of our web application.

```js
// Populate the buttons with terrestrial dates
buttons.forEach((button, index) => {
    button.textContent = marsDates[index];
    console.log("Mars Parameter Data:", parameterData.mars);
});
```
The line of code, `"Mars Parameter Data:", parameterData.mars`, has been strategically placed to provide real-time insight into the "Mars Parameter Data" and the contents of the `parameterData.mars` object.

This approach enables you to closely inspect the values and structure of this data during runtime. As a result, you can quickly identify any anomalies or errors, making it considerably easier to pinpoint and rectify issues within our codebase.
