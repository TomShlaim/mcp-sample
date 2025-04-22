# mcp-sample

A Python-based weather application that provides weather alerts and forecasts using the National Weather Service (NWS) API.

## Features

- Get active weather alerts for any US state
- Get detailed weather forecasts for any location using latitude and longitude within the US
- Uses official NWS API for accurate and reliable data
- Runs as an MCP server for seamless integration

## Important Note

This application uses the National Weather Service (NWS) API, which only provides weather data for locations within the United States. For international weather data, you would need to modify the application to use a different weather service API.

## Installation

This project requires Python 3.10 or higher. To install dependencies:

```bash
pip install .
```

## Usage

The application can be used in two ways: as a Python module or as an MCP server.

### Using as an MCP Server

The application is designed to run as an MCP server, which allows for seamless integration with MCP clients:

1. Run the server:
```bash
python weather.py
```

2. The server exposes two MCP tools:

- `get_alerts`: Get weather alerts for a US state
  ```python
  # Example MCP client usage
  result = await mcp.invoke("get_alerts", {"state": "CA"})
  ```

- `get_forecast`: Get weather forecast for coordinates
  ```python
  # Example MCP client usage
  result = await mcp.invoke("get_forecast", {
      "latitude": 37.7749,      # San Francisco coordinates
      "longitude": -122.4194
  })
  ```

### Using as a Python Module

You can also import and use the functions directly in your Python code:

#### Get Weather Alerts

Get active weather alerts for a US state using its two-letter state code:

```python
from weather import get_alerts

# Get alerts for California
alerts = await get_alerts("CA")
print(alerts)
```

#### Get Weather Forecast

Get a detailed weather forecast for a specific location using latitude and longitude:

```python
from weather import get_forecast

# Get forecast for San Francisco (approximate coordinates)
forecast = await get_forecast(37.7749, -122.4194)
print(forecast)
```

The forecast includes:
- Temperature
- Wind conditions
- Detailed forecast description
- 5-period forecast (typically covering the next few days)

## API Details

The application uses the National Weather Service (NWS) API. No API key is required, but we include a User-Agent header as per API requirements. The API only provides data for locations within the United States.
