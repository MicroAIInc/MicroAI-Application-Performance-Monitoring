# Features

### Deployment and Configurable Features

- **Seamless connectivity with elastic agent:** Captures data for metadata like environment, service name, APIs, transactions, spans and other details.
- **Secure Embedded Configuration:** Internal configurations are securely embedded into the agent binaries to prevent unauthorized access.
- **MQTT Data Transmission:** Securely transfers data using the MQTT protocol with built-in authentication.
- **Containerized Deployment:** Supports automatic deployment via Kubernetes and ECS for scalability.
- **Email Notifications:** Sends email notifications based on event severity.
- **External Data Exporter:** Exports collected data to third-party visualization tools.
- **Lightweight:** - Agent is design to be lightweight
- **Creativity at its best:** - Integrated always-on prometheus exporter allows the data to be available for prometheus server to capture and visualize it in any form on Grafana.
	- Setup Prometheus and Grafana click [here](Grafana-Extension.md)
## Monitoring Features

- **Dynamic learning as new endpoints are called** - Agent will learn about endpoints during the runtime
- **Each endpoint has a story** - Agent learns the behavior of each endpoints separately and monitors it.
- **Runs independently from the application** - Agent learns about the application

## Notifications and Alerts

- **Abnormal API transactions** Generates alerts for detected anomalies and publishes them to the launchpad.
- **Email Notification for Alerts:** Sends real-time email alerts.
- **External Exporter Alerts via HTTPS or Prometheus:** Sends alerts to external monitoring tools.