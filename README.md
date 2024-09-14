# KongFusion Application with Kong, Prometheus, and Grafana

This project contains a .NET Core Web API (KongFusion) that integrates with Kong API Gateway, Prometheus for monitoring, and Grafana for visualization. The application is designed to run multiple instances of the Web API, all managed through Docker Compose.

## Table of Contents
- [Project Structure](#project-structure)
- [Technologies Used](#technologies-used)
- [Prerequisites](#prerequisites)
- [Setup Instructions](#setup-instructions)
- [Docker Services](#docker-services)
- [Monitoring and Visualization](#monitoring-and-visualization)
- [Kong API Gateway](#kong-api-gateway)
- [Metrics Collection with Prometheus](#metrics-collection-with-prometheus)
- [Visualization with Grafana](#visualization-with-grafana)
- [License](#license)

## Project Structure

```
.
├── KongFusion/
│   ├── Controllers/
│   ├── Program.cs
│   └── KongFusion.csproj
├── docker-compose.yml
├── config/
│   ├── kong.yaml
│   └── prometheus.yml
├── README.md
└── .gitignore
```

## Technologies Used
- **Docker**: Containerize and manage multiple instances of the application.
- **Docker Compose**: Orchestrates services like Kong API Gateway, Prometheus, Grafana, and PostgreSQL.
- **Kong**: API Gateway to route traffic between services.
- **Prometheus**: Metrics collection for monitoring.
- **Grafana**: Visualization dashboard for monitoring data.
- **PostgreSQL**: Database backend for Kong.

## Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/emreesahiiinn/KongFusion.git
cd KongFusion
```

### 2. Build and run the Docker containers
To start the application and its services, run the following command:
```bash
docker-compose up
```
This command will:
- Build the `kongfusion` app.
- Start Kong, Prometheus, Grafana, and PostgreSQL containers.

### 3. Access the services

- **Kong Admin GUI**: [http://localhost:8002](http://localhost:8002)
- **Kong Admin API**: [http://localhost:8001](http://localhost:8001)
- **Kong Proxy**: [http://localhost:8000](http://localhost:8000)
- **Prometheus**: [http://localhost:9090](http://localhost:9090)
- **Grafana**: [http://localhost:3000](http://localhost:3000) (Default username: `admin`, password: `admin`)

### 4. Running multiple instances of the API

By default, the `docker-compose.yml` file spins up five instances of the `kongfusion` Web API. These instances are exposed on the following ports:
- **kongfusion-1**: [http://localhost:5071](http://localhost:5071)
- **kongfusion-2**: [http://localhost:5072](http://localhost:5072)
- **kongfusion-3**: [http://localhost:5073](http://localhost:5073)
- **kongfusion-4**: [http://localhost:5074](http://localhost:5074)
- **kongfusion-5**: [http://localhost:5075](http://localhost:5075)

## Docker Services

- **kongfusion**: The ASP.NET Core Web API application. It exposes endpoints and is load-balanced by Kong.
- **kong**: Kong API Gateway, configured to manage and route the requests between services.
- **db**: PostgreSQL database for storing Kong configurations.
- **prometheus**: Collects metrics from the `kongfusion` app for monitoring.
- **grafana**: Provides a dashboard for visualizing the metrics collected by Prometheus.

## Monitoring and Visualization

### Kong API Gateway
The Kong API Gateway is used to route traffic to multiple instances of the `kongfusion` application.

- Kong Admin GUI: [http://localhost:8002](http://localhost:8002)
- Kong Admin API: [http://localhost:8001](http://localhost:8001)
  
Kong is configured declaratively using the file `config/kong.yaml`.

### Metrics Collection with Prometheus
Prometheus collects metrics from each `kongfusion` instance. The configuration for Prometheus is defined in `config/prometheus.yml`.

Prometheus is available at [http://localhost:9090](http://localhost:9090).

### Visualization with Grafana
Grafana is used to visualize the metrics collected by Prometheus. Once the service is running, you can access the Grafana dashboard at [http://localhost:3000](http://localhost:3000).

To add Prometheus as a data source in Grafana:
1. Go to `Connections` > `Data Sources`.
2. Add a new Prometheus data source with the URL `http://prometheus:9090`.

You can then create custom dashboards based on the collected metrics.