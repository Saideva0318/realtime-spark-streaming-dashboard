# 🚀 Real-Time Spark Streaming Dashboard

![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-231F20?style=for-the-badge&logo=apachekafka&logoColor=white)
![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white)

## 📋 Project Overview

A production-grade real-time data streaming and analytics dashboard that processes IoT sensor data using Apache Spark Streaming and visualizes insights through interactive dashboards. This project demonstrates end-to-end streaming data pipeline architecture with real-time processing capabilities.

## 🏗️ Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  IoT Sensors    │────▶│  Apache Kafka    │────▶│  Spark Streaming│
│  (Data Source)  │     │  (Message Queue) │     │  (Processing)   │
└─────────────────┘     └──────────────────┘     └─────────────────┘
                                                           │
                                                           ▼
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  Grafana/       │◀────│  Time-Series DB  │◀────│  Data Transform │
│  Power BI       │     │  (InfluxDB)      │     │  & Aggregation  │
└─────────────────┘     └──────────────────┘     └─────────────────┘
```

## ✨ Key Features

- **Real-time Data Ingestion**: Continuous streaming from IoT sensors
- **Stream Processing**: Apache Spark Streaming for data transformation
- **Windowing Operations**: Time-based aggregations and analytics
- **Live Visualization**: Interactive dashboards with Grafana and Power BI
- **Scalable Architecture**: Horizontally scalable microservices design
- **Fault Tolerance**: Kafka for reliable message delivery
- **Monitoring & Alerts**: Real-time anomaly detection

## 🛠️ Technologies Used

### Data Processing
- **Apache Spark 3.4+**: Distributed stream processing
- **PySpark**: Python API for Spark
- **Apache Kafka**: Distributed messaging system
- **Kafka Streams**: Stream processing library

### Data Storage
- **InfluxDB**: Time-series database
- **Redis**: In-memory caching
- **PostgreSQL**: Metadata storage

### Visualization
- **Grafana**: Real-time dashboard
- **Power BI**: Business intelligence reporting
- **Plotly**: Interactive visualizations

### DevOps & Tools
- **Docker**: Containerization
- **Docker Compose**: Multi-container orchestration
- **Python 3.9+**: Primary programming language
- **Git**: Version control

## 📁 Project Structure

```
realtime-spark-streaming-dashboard/
│
├── src/
│   ├── data_generator/
│   │   ├── iot_sensor_simulator.py
│   │   └── config.yaml
│   ├── streaming/
│   │   ├── spark_consumer.py
│   │   ├── transformations.py
│   │   └── windowing.py
│   ├── kafka/
│   │   ├── producer.py
│   │   └── topics.py
│   └── utils/
│       ├── logger.py
│       └── helpers.py
│
├── dashboards/
│   ├── grafana/
│   │   ├── dashboard.json
│   │   └── datasources.yaml
│   └── powerbi/
│       └── template.pbix
│
├── config/
│   ├── spark-defaults.conf
│   ├── kafka-config.properties
│   └── influxdb.conf
│
├── docker/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── requirements.txt
│
├── tests/
│   ├── test_streaming.py
│   └── test_transformations.py
│
├── notebooks/
│   └── data_exploration.ipynb
│
├── docs/
│   ├── architecture.md
│   ├── setup_guide.md
│   └── api_reference.md
│
├── screenshots/
│   ├── dashboard_overview.png
│   └── architecture_diagram.png
│
├── README.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

## 🚀 Setup Instructions

### Prerequisites
- Python 3.9 or higher
- Apache Spark 3.4+
- Docker & Docker Compose
- Apache Kafka 3.0+
- 8GB RAM minimum

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Saideva0318/realtime-spark-streaming-dashboard.git
cd realtime-spark-streaming-dashboard
```

2. **Create virtual environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

4. **Start services with Docker Compose**
```bash
cd docker
docker-compose up -d
```

5. **Configure environment variables**
```bash
cp .env.example .env
# Edit .env with your configurations
```

6. **Initialize Kafka topics**
```bash
python src/kafka/topics.py --create
```

7. **Start the data generator**
```bash
python src/data_generator/iot_sensor_simulator.py
```

8. **Launch Spark Streaming job**
```bash
spark-submit --master local[*] \
  --packages org.apache.spark:spark-sql-kafka-0-10_2.12:3.4.0 \
  src/streaming/spark_consumer.py
```

9. **Access Grafana Dashboard**
```
URL: http://localhost:3000
Username: admin
Password: admin
```

## 📊 Sample Output

### Real-Time Metrics Dashboard
![Dashboard Overview](screenshots/dashboard_overview.png)

### Key Metrics Tracked
- **Sensor Readings**: Temperature, humidity, pressure
- **Throughput**: Messages per second
- **Latency**: End-to-end processing time
- **Anomalies**: Real-time alert detection
- **System Health**: Resource utilization

## 🔧 Configuration

### Spark Streaming Configuration
```python
# spark-defaults.conf
spark.streaming.stopGracefullyOnShutdown=true
spark.streaming.backpressure.enabled=true
spark.streaming.kafka.maxRatePerPartition=1000
spark.sql.streaming.metricsEnabled=true
```

### Kafka Producer Settings
```python
# kafka-config.properties
bootstrap.servers=localhost:9092
acks=all
retries=3
batch.size=16384
compression.type=snappy
```

## 📈 Performance Optimization

- **Batch Interval**: 5 seconds for optimal throughput
- **Parallelism**: 8 executors with 2 cores each
- **Memory**: 4GB per executor
- **Checkpointing**: Every 30 seconds
- **State Management**: RocksDB for state store

## 🧪 Testing

Run unit tests:
```bash
pytest tests/ -v --cov=src
```

Run integration tests:
```bash
python -m pytest tests/integration/ -v
```

## 📝 Future Enhancements

- [ ] Add machine learning models for predictive analytics
- [ ] Implement automatic scaling based on load
- [ ] Integration with AWS Kinesis
- [ ] Add support for multiple data sources
- [ ] Implement data quality checks
- [ ] Add authentication and authorization
- [ ] Create REST API for dashboard queries
- [ ] Add support for custom alerting rules
- [ ] Implement data lineage tracking
- [ ] Add A/B testing framework

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👤 Author

**Sai Deva Puttur**
- GitHub: [@Saideva0318](https://github.com/Saideva0318)
- LinkedIn: [Sai Deva Puttur](https://linkedin.com/in/sai-deva-puttur)

## 🙏 Acknowledgments

- Apache Spark community for excellent documentation
- Confluent for Kafka best practices
- Grafana Labs for visualization tools
- Real-time analytics community for inspiration

## 📞 Contact

For questions or feedback, please open an issue or reach out via LinkedIn.

---

⭐ **If you find this project useful, please consider giving it a star!** ⭐
