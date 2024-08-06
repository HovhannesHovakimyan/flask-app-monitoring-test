
# Flask App with Logging Using OpenTelemetry, Alloy, Loki, Promtail, and Grafana



## System Requirements



- Docker and Docker Compose installed

- Minimum 4 GB RAM

- 2 CPU cores

- Internet connection to pull Docker images



## Deployment & Teardown Manual


### Step 1: Clone the Repository
Deploy  the  stack  using  Docker  Compose:

1. git  clone  https://github.com/HovhannesHovakimyan/monitoring-test.git
2. cd  monitoring-test
3. Use `docker-compose  up  --build` (or  `docker-compose  up  -d`  for  a  detached  mode) commands to start the deployment.


Depending on your system, give it a minute to deploy and verify the components of the deployed services.

- Alloy
http://localhost:4317/clustering
- Promtail
http://localhost:9080/targets
- Loki
http://localhost:3100/ready (you should see `ready` when the system is ready)
http://localhost:3100/metrics
- Grafana
http://localhost:3000/

### Step 2: How to Test the Solution
1. Open your browser and navigate to `http://localhost:8080/get` to generate a GET request log.
2. Use `curl` to send a POST request: `curl -X POST http://localhost:8080/post`
3. You should see logs from your Flask application in Grafana's `Loki Logs Dashboard`.

### Step 3: Remove the deployment
1. Stop the deployment using `Ctrl + C` keys combination if the deployment was started in the interactive mode.
2. Use `docker-compose down` command to remove the deployment.

## Service Diagram
```
+----------------+    +--------------+    +------+    +--------+    +--------+
| Flask App      | -> | OpenTelemetry| -> | Alloy| -> | Loki   | -> | Grafana|
+----------------+    +--------------+    +------+    +--------+    +--------+
                       ^                        |
                       |                        |
                       +------------------------+
                                 Promtail
```

-   **Flask App**: Generates logs.
-   **OpenTelemetry**: Collects and exports logs.
-   **Alloy**: Receives logs from OpenTelemetry.
-   **Promtail**: Scrapes logs and pushes them to Loki.
-   **Loki**: Stores and indexes logs.
-   **Grafana**: Visualizes logs from Loki.