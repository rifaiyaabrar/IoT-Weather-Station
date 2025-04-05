# IoT Weather Station

A real-time weather monitoring system built using Raspberry Pi Pico W and BMP280 sensor with MQTT protocol for data transmission and InfluxDB for storage.

## Overview

This IoT Weather Station project uses the latest IoT technologies to capture and assess weather data in real-time. It aims to gather weather data, process it efficiently, and make it accessible to users through a user-friendly interface. The project demonstrates how wireless communication, cloud services, and sensors can be combined to provide accurate information on weather conditions.

## Architecture

The IoT Weather Station architecture comprises three main layers:

### Sensor Layer
- Implements the BMP280 sensor for measuring temperature and atmospheric pressure
- Uses Raspberry Pi Pico W as the hub for collecting and pre-processing data

### Networking Layer
- MQTT protocol for transferring data from Raspberry Pi Pico W to cloud server
- Wi-Fi connectivity through the built-in functionality of Pico W

### Data Management Layer
- Data storage and analysis in InfluxDB
- Historical trend visualization through Grafana

## Components

### Hardware
- Raspberry Pi Pico W microcontroller
- BMP280 temperature and pressure sensor
- 3.3V USB power source
- LED indicators
- OLED display (optional for local monitoring)

### Software
- MicroPython for firmware development (using Thonny)
- Python for back-end integration
- MQTT for lightweight and reliable message transmission
- Web technologies: HTML, CSS, and JavaScript for user dashboard
- InfluxDB for time-series data storage
- Grafana for data visualization

## Data Processing and Handling

### Data Collection
- BMP280 sensor readings are polled at regular intervals (approximately every 10 seconds)
- Raw sensor data is converted to appropriate units (°C for temperature, hPa for pressure)
- Initial data validation is performed on the Pico W to filter out anomalous readings

### Data Preprocessing
- Moving average filtering to reduce noise in sensor readings
- Calibration offsets applied to compensate for sensor-specific variations
- Timestamp generation for each data point to ensure accurate time-series analysis

### Data Transmission
- Data is packaged into JSON format for efficient MQTT transmission
- Example payload structure:
  ```json
  {
    "device_id": "weather_station_01",
    "timestamp": 1712323456,
    "temperature": 23.5,
    "pressure": 1013.25
  }
  ```
- Transmission frequency can be adjusted based on network conditions
- Timeout of 10ms implemented for each transmission to manage network resources

### Data Storage
- Time-series data is stored in InfluxDB with appropriate tags and fields
- Data retention policies configured for efficient storage management:
  - High-resolution data (10s intervals) kept for 7 days
  - Aggregated hourly averages kept for 3 months
  - Daily statistics kept indefinitely

### Data Analysis
- Real-time statistics calculation (min, max, average values)
- Threshold-based alerting system (LED activation when temperature exceeds 23°C)
- Historical trend analysis through InfluxDB queries
- Custom dashboards in Grafana for comprehensive data visualization

## Implementation Phases

1. **Basic Hardware Setup**
   - Assembly of hardware components and testing individual sensors
   - Configuration of OLED display and LED indicators

2. **Firmware Development**
   - Development of sensor reading functions and display routines

3. **Cloud Integration**
   - Setting up MQTT broker for data transmission
   - Establishing Wi-Fi connectivity for seamless communication

4. **Web View Development**
   - Design of an intuitive user interface for real-time data visualization
   - Implementation of MQTT client functionality in the local host

5. **Cloud Integration**
   - Integration with InfluxDB for data storage and analytics

6. **Testing and Optimization**
   - Testing with varying payload sizes and message volumes
   - System performance optimization for low-latency operations

## Performance Metrics

- **Latency**: 0.0029-0.0032 seconds under normal Wi-Fi conditions
- **Throughput**: 2.49 messages/second
- **Temperature Range**: Accurate readings between 5°C to 26°C
- **Update Frequency**: Under 10 seconds for parameter updates
- **Data Processing Efficiency**: Processes up to 1000-byte payloads with minimal latency increase

## Features

- Real-time monitoring of temperature and atmospheric pressure
- Cloud-based data storage for historical analysis
- Web-based dashboard for remote monitoring
- LED alerts for temperature thresholds (e.g., when temperature exceeds 23°C)
- Low power consumption for sustainable long-term deployment
- Robust data handling with error recovery mechanisms

## Strengths

- Real-time monitoring with accurate temperature and pressure readings
- Reliable cloud integration using MQTT protocol
- Cost-effective implementation using affordable hardware
- Historical data visualization through InfluxDB and Grafana
- Efficient data processing pipeline from sensor to dashboard

## Limitations

- BMP280 sensor may require reconnection to ensure data accuracy
- Dependency on stable Wi-Fi connectivity for data visualization and database updates

## Installation & Setup

1. **Hardware Assembly**
   - Connect BMP280 sensor to Raspberry Pi Pico W following the connection diagram

2. **Software Setup**
   ```
   # Clone the repository
   git clone https://github.com/rifaiyaabrar/iot-weather-station.git
   
   # Install required libraries for Raspberry Pi Pico W
   # Upload the MicroPython firmware using Thonny IDE
   ```

3. **MQTT Broker Configuration**
   ```python
   # Configure MQTT settings in config.py
   MQTT_BROKER = "your_mqtt_broker_address"
   MQTT_PORT = 1883
   MQTT_TOPIC = "weather/data"
   ```

4. **InfluxDB Setup**
   ```
   # Install InfluxDB on your server
   # Create a database for weather data
   # Configure connection parameters in the application
   ```

5. **Web Dashboard Setup**
   ```
   # Configure the localhost settings
   # Open the dashboard in a web browser
   ```

## Data Flow

```
BMP280 Sensor → Raspberry Pi Pico W → MQTT Broker → Backend Service → InfluxDB → Grafana Dashboard
                      ↓                                                   ↑
                 Local OLED                                        Web Interface
                   Display
```

## Usage

1. Power on the Raspberry Pi Pico W
2. The system will automatically connect to Wi-Fi and begin transmitting data
3. Access the web dashboard to view real-time and historical weather data
4. LED indicators will alert when temperature exceeds predefined thresholds
5. Query historical data through the Grafana interface for trend analysis

## Future Improvements

- Addition of more sensors (humidity, rainfall, wind speed)
- Enhanced power management for battery operation
- Mobile application development for easier access
- Machine learning integration for weather prediction
- Expansion to multiple monitoring stations for wider coverage
- Advanced data analytics for weather pattern recognition

## Contributors

- Surekha Medapati
- S M Rifaiya Abrar
- Minhaz Uddin
- Hooria Kiran


## References

1. MQTT.org. MQTT protocol specifications: https://mqtt.org
2. Kumar, R., Rani, S., & Sharma, N. (2019). Design and implementation of real-time weather monitoring system using IoT. IEEE Access.
3. InfluxData. Time-Series Database for IoT and Edge Systems: InfluxDB Official Site.
4. Grafana Labs. Grafana for IoT Dashboards and Monitoring. Official Website.
