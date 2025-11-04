# Prometheus & Grafana Setup for MicroAI Application Performance Monitoring

## Table of Contents

* [1. Download and Install Prometheus Server](#1-download-and-install-prometheus-server)
* [2. Setup Prometheus Server](#2-setup-prometheus-server)
* [3. Verify Prometheus and Agent Connectivity](#3-verify-prometheus-and-agent-connectivity)
* [4. Connecting Grafana with Prometheus Server](#4-connecting-grafana-with-prometheus-server)
* [5. Visualizing Agent Data](#5-visualizing-agent-data)

---

## 1. Download and Install Prometheus Server

1. Visit the official Prometheus download page: [https://prometheus.io/download/](https://prometheus.io/download/) and download the package for your operating system.

### For Linux:

```bash
wget https://github.com/prometheus/prometheus/releases/download/v3.5.0/prometheus-3.5.0.linux-amd64.tar.gz
tar -xvf prometheus-3.5.0.linux-amd64.tar.gz
```

---

## 2. Setup Prometheus Server

All MicroAI APM Agents export Prometheus metrics on port `9100`.

1. Open the `prometheus.yml` configuration file.
2. Add a new job under the `scrape_configs` section with the agent IPs as targets.

### Example:

```yaml
scrape_configs:
  - job_name: "MicroAI-APM"
    static_configs:
      - targets: ["XXX.XXX.XXX.XXX:9100", "XXX.XXX.XXX.XXX:9100"]
```

3. Save and close the configuration file.

4. Ensure the Prometheus binary has execute permissions:

```bash
chmod +x prometheus
```

5. Start Prometheus:

```bash
./prometheus
```

---

## 3. Verify Prometheus and Agent Connectivity

1. Access the Prometheus web interface (default port `9090`):

```
http://XXX.XXX.XXX.XXX:9090/
```

2. Navigate to **Status** → **Targets**.
3. Verify that the MicroAI Security and Monitoring agent appears as **UP**.

<img src="./images/Prometheus-Web-Interface.png" width="600" alt="Prometheus Web Interface Status">
---

## 4. Connecting Grafana with Prometheus Server

1. On the Grafana homepage, open the left panel.
2. Click on **Connections** → **Add new data source**.
3. Search for **Prometheus** and select it.
4. Under **Connection**, enter your Prometheus server URL:

```
http://XXX.XXX.XXX.XXX:9090
```

5. Click **Save & test**.
6. A confirmation message will indicate a successful connection.

<img src="./images/Grafana-Success.png" width="600" alt="Grafana Successful Connection">
---

## 5. Visualizing Agent Data

1. On the Grafana homepage, open the left panel.
2. Click **Dashboards** → **New** → **Import**.

<img src="./images/Grafana-Import.png" width="600" alt="Grafana Import">

3. Select the JSON dashboard files from the following path:

- [Landing Dashboard - APM.json](./templates/Landing%20Dashboard%20-%20APM.json)  
- [Service Detail Dashboard - APM.json](./templates/Service%20Detail%20Dashboard%20-%20APM.json)
- [Transaction Detail Dashboard - APM.json](./templates/Transaction%20Detail%20Dashboard%20-%20APM.json)
- [Transaction Traces Dashboard - APM.json](./templates/Transaction%20Traces%20Dashboard%20-%20APM.json)

4. Import the following dashboard files:

   * `Landing Dashboard - APM.json`
   * `Service Detail Dashboard - APM.json`
   * `Transaction Detail Dashboard - APM.json`
   * `Transaction Traces Dashboard - APM.json`

3. Once imported, you will see dashboards available.

<img src="./images/Grafana-Dashboard-List.png" width="600" alt="Grafana Dashboard List">

6. Click on **Landing Dashboard -APM** to view the complete dashboard.

<img src="./images/Landing-Dashboard.png" width="600" alt="APM Landing Page View">

<img src="./images/Service-Details.png" width="600" alt="Service View">

<img src="./images/Transaction-Details.png" width="600" alt="Transaction View">

<img src="./images/Transaction-Traces.png" width="600" alt="Transaction View">

---

**Note:** These dashboards are pre-built templates that work out-of-the-box with data from the MicroAI Application Performance Monitoring agent via Prometheus.
