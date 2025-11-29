
# Technical Documentation - OpenWeather API Integration

**Author:** Vanitha C N  
**Date:** 04/07/2025  
**Purpose:** Provide an in-depth reference for OpenWeather API integration, including base URLs, endpoints, parameters, responses, and best practices.

---

## 1. Introduction

The **OpenWeather API** provides access to global weather data - including **current conditions**, **forecasts**, **air pollution**, and **historical data**.  
It enables developers to integrate accurate meteorological information into applications for **weather dashboards**, **travel apps**, **IoT systems**, or **data analytics**.

---

## 2. Base URLs and Authentication

All OpenWeather APIs require an **API key (`appid`)** for authentication.  
Include the key in every request query string, for example:

```
?appid=YOUR_API_KEY
```

You can also specify:

- `units` ->`standard`, `metric`, or `imperial`  
- `lang` -> Language code (e.g., `en`, `de`, `fr`)

### Base URLs

| API Service | Base URL |
|--------------|-----------|
| **Current Weather Data (v2.5)** | `https://api.openweathermap.org/data/2.5/` |
| **One Call API (v3.0)** | `https://api.openweathermap.org/data/3.0/onecall` |
| **5 Day / 3 Hour Forecast** | `https://api.openweathermap.org/data/2.5/forecast` |
| **Air Pollution API** | `https://api.openweathermap.org/data/2.5/air_pollution` |

---

## 3. Endpoints and Request Details

### 3.1 Current Weather Data

**Endpoint:**  
```
GET /data/2.5/weather
```

**Description:**  
Retrieves real-time weather conditions for a city, geographic coordinates, or ZIP code.

#### Parameters

| Parameter | Required | Description |
|------------|-----------|-------------|
| `q` | Yes | City name and optional country code (e.g., `London,uk`) |
| `lat`, `lon` | Yes (alternative) | Geographic coordinates |
| `zip` | Optional | ZIP or postal code with country code |
| `appid` | Yes | Your API key |
| `units` | No | Units of measurement (`standard`, `metric`, `imperial`) |
| `lang` | No | Response language code |

#### Example Request
```
https://api.openweathermap.org/data/2.5/weather?q=Berlin&units=metric&appid=YOUR_API_KEY
```

#### Example JSON Response
```json
{
  "coord": {"lon": 13.41, "lat": 52.52},
  "weather": [{"id": 803, "main": "Clouds", "description": "broken clouds"}],
  "main": {"temp": 18.3, "feels_like": 17.8, "pressure": 1012, "humidity": 60},
  "wind": {"speed": 3.6, "deg": 270},
  "name": "Berlin",
  "cod": 200
}
```

---

### 3.2 5 Day / 3 Hour Forecast

**Endpoint:**  
```
GET /data/2.5/forecast
```

**Description:**  
Provides forecast data for 5 days with 3-hour intervals.

#### Example Request
```
https://api.openweathermap.org/data/2.5/forecast?q=Berlin&appid=YOUR_API_KEY
```

#### Example JSON Response
```json
{
  "city": {"name": "Berlin", "country": "DE"},
  "list": [
    {"dt": 1751626864, "main": {"temp": 18.1}, "weather": [{"description": "clear sky"}]},
    {"dt": 1751630464, "main": {"temp": 17.3}, "weather": [{"description": "few clouds"}]}
  ]
}
```

---

### 3.3 One Call API (v3.0)

**Endpoint:**  
```
GET /data/3.0/onecall
```

**Description:**  
Returns comprehensive weather data (current, hourly, daily, and alerts) for a specific location.

#### Example Request
```
https://api.openweathermap.org/data/3.0/onecall?lat=33.44&lon=-94.04&appid=YOUR_API_KEY
```

#### Example JSON Response
```json
{
  "lat": 33.44,
  "lon": -94.04,
  "current": {"temp": 289.5, "weather": [{"description": "light rain"}]},
  "daily": [
    {"dt": 1751716864, "temp": {"min": 285.1, "max": 293.2}}
  ]
}
```

---

### 3.4 Air Pollution API

**Endpoint:**  
```
GET /data/2.5/air_pollution
```

**Description:**  
Returns air quality index (AQI) and pollutant concentrations by location.

#### Example Request
```
https://api.openweathermap.org/data/2.5/air_pollution?lat=50&lon=14&appid=YOUR_API_KEY
```

#### Example JSON Response
```json
{
  "coord": {"lon": 14, "lat": 50},
  "list": [
    {
      "main": {"aqi": 2},
      "components": {
        "co": 203.7,
        "no2": 14.2,
        "o3": 68.4
      }
    }
  ]
}
```

---

## 4. Response Field Definitions

| Field | Type | Description |
|--------|------|-------------|
| `coord.lon` | float | Longitude of location |
| `coord.lat` | float | Latitude of location |
| `weather[].main` | string | Group of weather parameters |
| `weather[].description` | string | Weather condition description |
| `main.temp` | float | Temperature (in selected units) |
| `main.humidity` | integer | Humidity (%) |
| `wind.speed` | float | Wind speed |
| `wind.deg` | integer | Wind direction (degrees) |
| `dt` | integer | Timestamp (Unix UTC) |
| `aqi` | integer | Air Quality Index (1-5 scale) |

---

## 5. Example Integration Flow

1. **Get current weather:**  
   `GET /weather?q=CityName&units=metric&appid=API_KEY`

2. **Extract coordinates (lat, lon)** from response.

3. **Fetch extended data:**  
   `GET /onecall?lat={lat}&lon={lon}&exclude=minutely&appid=API_KEY`

4. **Display current, hourly, and daily weather** in app dashboard.

5. **Optionally fetch AQI data:**  
   `GET /air_pollution?lat={lat}&lon={lon}&appid=API_KEY`

6. **Handle and cache responses** for performance optimization.

---

## 6. Best Practices

-  Always **protect your API key** from public exposure.
-  Use **caching** to minimize redundant API calls.
-  **Convert timestamps** (e.g., `dt`, `sunrise`, `sunset`) to human-readable local time.
-  Apply **units** and **lang** parameters to localize your app’s data presentation.
-  Implement **error handling** for HTTP codes:
  - `401 Unauthorized` -> Invalid or missing API key  
  - `404 Not Found` -> Invalid location or endpoint  
  - `429 Too Many Requests` -> Rate limit exceeded
-  For One Call API, use the `exclude` parameter to avoid unnecessary data (e.g., `exclude=minutely,hourly`).
-  For frequent updates, implement **data caching** or **scheduled refreshes**.

---

## 7. Summary

The **OpenWeather API** offers a comprehensive suite of weather and air quality data services.  
This documentation outlines endpoints, request structures, response formats, and best practices to guide developers in integrating the API efficiently.

**Key Features:**
- Multiple data layers (Current, Forecast, Pollution)
- Flexible parameter options (units, language)
- JSON responses optimized for web and mobile applications
- Developer-friendly design for fast integration

---

### References

- [OpenWeather Official Documentation](https://openweathermap.org/api)
- [One Call API 3.0 Guide](https://openweathermap.org/api/one-call-3)
- [Air Pollution API Docs](https://openweathermap.org/api/air-pollution)
- [Current Weather Data API](https://openweathermap.org/current)
