# Health Anomaly Detector Stack

A comprehensive monitoring solution for health vitals using a modern observability stack. This project simulates wearable health devices and provides real-time monitoring, anomaly detection, and visualization capabilities.

## Architecture

### Architecture Diagram
![System Architecture](./media/architecture_diagram.png)

### System Components

The stack consists of five main components that work together to collect, process, store, and visualize health vitals data:

- **[Health Sensor Simulator](https://github.com/marcoom/health-sensor-simulator/)** - Simulates wearable devices generating vital signs data and sends alert when an anomaly is detected
- **Telegraf** - Data collection agent that polls vitals and forwards data to InfluxDB
- **InfluxDB 3** - Time-series database for storing health metrics
- **Grafana** - Visualization platform with custom health dashboards
- **InfluxDB3 Explorer** - Database browser for easy data exploration

## Features

- 🫀 **Real-time Health Monitoring** - Continuous collection of vital signs (heart rate, blood pressure, temperature, etc.)
- 🚨 **Anomaly Detection** - Built-in anomaly detection with configurable thresholds
- 📊 **Interactive Dashboards** - Custom Grafana dashboards with health-specific icons
- 🔍 **Data Exploration** - Web-based database browser for data analysis
- 🐳 **Containerized Deployment** - Complete stack runs with Docker Compose
- ⚙️ **Configurable** - Environment-based configuration for different deployment scenarios

## Quick Start

### Prerequisites
- Docker and Docker Compose
- Git

### Initial Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/marcoom/health-anomaly-detector-stack
   cd health-anomaly-detector-stack
   ```

2. **Configure environment variables**
   ```bash
   cp .env.template .env
   ```
   
3. **Start the services**
   ```bash
   docker compose up -d
   ```

4. **Generate InfluxDB token** (Required for first-time setup)
   ```bash
   docker compose exec influxdb influxdb3 create token
   ```
   
5. **Update .env file**
   Copy the generated token and update the `INFLUXDB_TOKEN` variable in your `.env` file:
   ```bash
   INFLUXDB_TOKEN=your-generated-token-here
   ```

6. **Restart the stack**
   ```bash
   docker compose down
   docker compose up -d
   ```

## Access Points

Once the stack is running, access the following services:

| Service | URL | Description |
|---------|-----|-------------|
| **Health Simulator (UI)** | `http://localhost:8501` | Streamlit interface for the health sensor |
| **Grafana** | `http://localhost:3000` | Dashboards and visualization (admin/password) |
| **Health Simulator (API)** | `http://localhost:8000` | FastAPI endpoints for vitals data |
| **InfluxDB** | `http://localhost:8181` | Time-series database |
| **InfluxDB Explorer** | `http://localhost:8888` | Database browser and query interface |

## Configuration

### Environment Variables

The stack is configured through environment variables defined in `.env`. Key configurations include:

```bash
# Health Sensor Simulator
STREAMLIT_PORT=8501
FASTAPI_PORT=8000
DATA_GENERATION_INTERVAL_SECONDS=5
ANOMALY_DETECTION_METHOD=EIF  # Extended Isolation Forest
EIF_THRESHOLD=0.4

# InfluxDB
INFLUXDB_PORT=8181
INFLUXDB_TOKEN=your-influxdb-token-here
INFLUXDB_BUCKET=health
INFLUXDB_ORG=health_org

# Grafana
GRAFANA_ADMIN_USER=admin
GRAFANA_ADMIN_PASSWORD=password

# Telegraf
TELEGRAF_COLLECTION_INTERVAL=5s
```

## Usage

### Monitoring Health Data

1. **View Real-time Data**: Access the Streamlit interface to configure live vitals generation
2. **Analyze Trends and Alerts**: Open Grafana dashboards to visualize health metrics over time

### Common Commands

```bash
# View logs for specific services
docker compose logs -f health-sensor-simulator
docker compose logs -f telegraf
docker compose logs -f influxdb
docker compose logs -f grafana

# Restart specific service
docker compose restart <service-name>

# Stop the entire stack
docker compose down

# Remove all data (including InfluxDB volumes)
docker compose down -v
```

## Development

### Project Structure

```
health-anomaly-detector-stack/
├── compose.yml                 # Docker Compose configuration
├── .env.template              # Environment variables template
├── grafana/
│   ├── configs/              # Grafana configuration files
│   ├── dashboards/           # Dashboard definitions
│   └── icons/                # Custom health-related icons
└── telegraf/
    ├── telegraf.conf         # Telegraf configuration
    └── sample-telegraf.conf  # Sample configuration
```

## Troubleshooting

### Common Issues

1. **InfluxDB Connection Errors**: Ensure the token is properly generated and configured in `.env`
2. **Port Conflicts**: Check that configured ports are not in use by other services
3. **Volume Permissions**: Ensure Docker has proper permissions for volume mounts

## License
This project is licensed under the **MIT License** — you are free to use, modify, and distribute it, with attribution. See the [LICENSE](LICENSE) file for details.

## Related Projects

- **[Health Sensor Simulator](https://github.com/marcoom/health-sensor-simulator/)** - The core health data generation component

---

For issues, questions, or contributions, please refer to the project's issue tracker.