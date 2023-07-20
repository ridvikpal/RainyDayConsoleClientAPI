# RainyDay (Console Version)

## Introduction
RainyDay is a simple weather application that provides complete weather information built in Java. It utilizes
the free [WeatherAPI](https://www.weatherapi.com/) as the information source and utilizes the
[gson](https://github.com/google/gson) library for JSON serialization and deserialization. This version is purely
a console version; it doesn't include the JavaFX GUI that the general RainyDay Application has. However, it does have
all the same functionality for data retrieval:

![program_start.png](pictures/program_start.png)

In addition to simply viewing the weather data, it also provides stores the data in separate classes.
Therefore, this code from those classes can be easily modified for use in any application requiring 
weather information. Therefore, the classes in the console version are the backbone of the GUI vesion.

## Features
All the features and their associated commands are shown upon application startup. These features are `CURRENT`, 
`FORECAST`, `ASTRONOMY`, `SEARCH`. Of course, you can also exit the application with `EXIT`. Additionally, the
commands are case-insensitive. This means that `forecast` is the same as `FORECAST`, similar to SQL commands.
Note that whenever a location is required for a command, it can be provided in the following forms and is
case-insensitive:

<div align="center">

| Type               | Example                |
|--------------------|------------------------|
| City Name          | Toronto                |
| Specific City Name | toronto-ontario-canada |
| Postal Code        | 90210                  |
| IP Address         | 192.158.1.38           |
| Longitude/Latitude | 38.8/-77.03            |

</div>

### Current Weather
The current weather data for a location can be found with the `CURRENT` command. This command takes in a location.

![current.png](pictures/current.png)

### Forecasted Weather
The forecasted weather can be found with the `FORECAST` command. Since I'm using
the free version of WeatherAPI, the program is limited to viewing only up to 3 days from the current day with a 
forecast request. This can be improved if you replace the key with an upgraded account key in the `Connection.java`
file. This command takes in a location and then the number of days to forecast. This command gets both the current
weather and the forecasted weather.

![forecast.png](pictures/forecast.png)

### Astronomy
Weather-related astronomy can be found with the `ASTRONOMY` command. This command takes in a location and a date
to get the astronomy for.

![astronomy.png](pictures/astronomy.png)

### Searching Weather Database
The WeatherAPI database can be searched for using the `SEARCH` command. This command is useful to figure out the
complete name for the location you want to get information for:

![search.png](pictures/search.png)

## Data Organization
As mentioned, the data from WeatherAPI is deserialized into various classes, and these classes are modular and portable 
such that they can be used in any application for weather data. These classes are:

| Class                 | Description                                            | Parent Classes             |
|-----------------------|--------------------------------------------------------|----------------------------|
| `Weather`             | Stores all weather information from the API            | None                       |
| `Location`            | Stores location information                            | `Weather`                  |
| `Current`             | Stores all current weather information                 | `Weather`                  |
| `Forecast`            | Stores all forecasted weather information              | `Weather`                  |
| `Alert`               | Stores all emergency weather alerts                    | `Weather`                  |
| `Astronomy`           | Stores all weather astronomy information               | `Weather`                  |
| `Condition`           | Stores the current weather condition information       | `Current`, `Hour`, `Day`   |
| `AirQuality`          | Stores the air quality information                     | `Current`, `Hour`, `Day`   |
| `ForecastDay`         | Stores the forecast for a specific day                 | `Forecast`                 |
| `Hour`                | Stores the weather for particular hour in the forecast | `ForecastDay`              |
| `Day`                 | Stores the weather for a particular day                | `ForecastDay`              |
| `Astro`               | Stores the weather astronomy                           | `Astronomy`, `ForecastDay` |
| `AutoCompleteElement` | Stores the location search information                 | None                       |

### Organization Diagram
This can be better represented in the following diagram:

