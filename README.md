
# Flask App with Logging Using OpenTelemetry, Alloy, Loki, Promtail, and Grafana



## System Requirements



- Docker and Docker Compose installed

- Minimum 4 GB RAM

- 2 CPU cores

- Internet connection to pull Docker images



## Deployment Manual



### Step 1: Clone the Repository



```sh

git  clone  https://github.com/HovhannesHovakimyan/monitoring-test.git

cd  monitoring-test
```




### Step 2: Clone the Repository



Deploy  the  stack  using  Docker  Compose:



docker-compose  up  --build

or  docker-compose  up  -d  for  a  detached  mode


Give it a minute to spin up.
Check the components of the services deployed.

- Alloy
http://localhost:4317/clustering
- Promtail
http://localhost:9080/targets
- Loki
http://localhost:3100/ready
http://localhost:3100/metrics
- Grafana
http://localhost:3000/

### How to Test the Solution
1. Open your browser and navigate to `http://localhost:8080/get` to generate a GET request log.
2. Use `curl` to send a POST request: `curl -X POST http://localhost:8080/post`
3. You should see logs from your Flask application in Grafana's `Loki Logs Dashboard`.

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