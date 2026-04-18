# 🏃 Vienna Half Marathon – Wind Analysis

An interactive, client-side web tool that analyzes wind conditions for the Vienna City Half Marathon.

## Features

- **GPS Track**: Loads the **GPX track** (`WienerStaedtischeHalbmarathon.gpx`) and displays it on an interactive Leaflet map
- **Wind Forecast**: Fetches real-time wind forecasts from [Open-Meteo](https://open-meteo.com/) (free, no API key required)
- **Time-Varying Wind**: Specify your expected runtime and the tool accounts for wind changes during the race by interpolating hourly forecasts based on your pace
- **Heatmap Visualization**: Colors the track green (tailwind), red (headwind), or yellow (crosswind) based on wind direction relative to running direction
- **Path Integral**: Computes the net wind effect over the entire track by integrating the wind component along the running direction
- **Wind Profile Chart**: Shows headwind/tailwind intensity along the track distance
- **Temperature Profile Chart**: Shows the forecasted temperature along the track distance, accounting for time-varying conditions during the race
- **Sun Intensity Chart**: Shows the forecasted solar radiation (shortwave radiation in W/m²) along the track distance
- **Rain Amount Chart**: Shows the forecasted precipitation (mm) along the track distance

## How to Use

1. Open `index.html` in any modern web browser
2. The GPX track is automatically loaded from the local `WienerStaedtischeHalbmarathon.gpx` file
3. Set the race date and start time (defaults to April 19, 2026 at 09:00)
4. Set your expected runtime (defaults to 1:45 for a half marathon)
5. Click **"Load Wind Forecast"** to fetch the latest wind data
6. Explore the heatmap on the map and review the path integral results

## How it Works

The tool computes the dot product of the wind vector with the running direction at each track segment:

```
wind_component = wind_speed × cos(wind_direction_to − running_bearing)
```

**Time-varying wind:** When a runtime is specified, the tool assumes a constant pace and
interpolates hourly wind forecasts for each track segment based on when the runner would
reach that point. Wind speed is linearly interpolated and wind direction is interpolated
along the shortest angular arc.

The **path integral** averages the wind component over the total distance:

```
avg_wind_effect = (1/D) × Σ (wind_component_i × segment_length_i)
```

- **Positive** result → net tailwind (favorable)
- **Negative** result → net headwind (unfavorable)
- **Near zero** → balanced or mostly crosswind

## Tech Stack

- Pure HTML/CSS/JavaScript (no build step, no backend)
- [Leaflet.js](https://leafletjs.com/) for the interactive map
- [Open-Meteo API](https://open-meteo.com/) for wind forecasts
- [OpenStreetMap](https://www.openstreetmap.org/) for map tiles
- Official GPX track from [Vienna City Marathon](https://www.vienna-marathon.com/)
