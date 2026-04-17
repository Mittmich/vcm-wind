# 🏃 Vienna Half Marathon – Wind Analysis

An interactive, client-side web tool that analyzes wind conditions for the Vienna City Half Marathon.

## Features

- **GPS Track**: Loads the **official GPX track** from [vienna-marathon.com](https://www.vienna-marathon.com/var/upload/public/2026/WienerStaedtischeHalbmarathon.gpx) at runtime and displays it on an interactive Leaflet map
- **Wind Forecast**: Fetches real-time wind forecasts from [Open-Meteo](https://open-meteo.com/) (free, no API key required)
- **Heatmap Visualization**: Colors the track green (tailwind), red (headwind), or yellow (crosswind) based on wind direction relative to running direction
- **Path Integral**: Computes the net wind effect over the entire track by integrating the wind component along the running direction
- **Wind Profile Chart**: Shows headwind/tailwind intensity along the track distance

## How to Use

1. Open `index.html` in any modern web browser
2. The official GPX track is automatically loaded from vienna-marathon.com
3. Set the race date and start time (defaults to April 19, 2026 at 09:00)
4. Click **"Load Wind Forecast"** to fetch the latest wind data
5. Explore the heatmap on the map and review the path integral results

## How it Works

The tool computes the dot product of the wind vector with the running direction at each track segment:

```
wind_component = wind_speed × cos(wind_direction_to − running_bearing)
```

The **path integral** averages this component over the total distance:

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
