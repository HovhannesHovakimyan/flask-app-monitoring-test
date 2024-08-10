
# Flask App with Logging Using OpenTelemetry, Alloy, Loki, Promtail, and Grafana



## System Requirements



- Docker, Docker Compose and CURL installed

- Minimum 4 GB RAM

- 2 CPU cores

- Internet connection to pull Docker images



## Deployment & Teardown Manual


### Step 1: Deploy the solution
Deploy  the  stack  using  Docker  Compose:

1. git  clone  https://github.com/HovhannesHovakimyan/flask-app-monitoring-test.git
2. cd  monitoring-test
3. Use `docker-compose  up  --build` for interactive mode (or  `docker-compose  up  -d`  for  a  detached  mode) command to start the deployment.
4. This will deploy Flask Dummy app, Grafana (with default datasource and dashbaord configured), Alloy, Promtail, and Loki.


Depending on your system, give it a minute to deploy and verify the components of the deployed services.

- Alloy
http://localhost:12345/clustering
- Promtail
http://localhost:9080/targets
- Loki
http://localhost:3100/ready (you should see `ready` when the system is ready)
http://localhost:3100/metrics
- Grafana
http://localhost:3000/


### Step 2: How to Test the Solution

1. Using CLI, let's make 100 GET and 50 POST requests to the Flask Dummy app.
2. For Linux/macOS
`
for i in {1..100}; do
    curl http://localhost:8080/get
done
`
3. For Windows (starting from Windows 10 version 1803 and Windows Server 2019)
`
for i in {1..100}; do
    curl http://localhost:8080/get
done
`
4. For Linux/macOS
`
for i in {1..100}; do
    curl +X POST http://localhost:8080/post
done
`
5. For Windows (starting from Windows 10 version 1803 and Windows Server 2019)
`
for i in {1..100}; do
    curl +X POST http://localhost:8080/post
done
`
6. You should see logs from your Flask Dummy application in Grafana's `Loki Logs Dashboard`.


### Step 3: Remove the solution
1. Stop the deployment using `Ctrl + C` keys combination if the deployment was started in the interactive mode.
2. Use `docker-compose down` command to remove the deployment.

## Service Diagram
```
+----------------+    +--------------+    +------+    +--------+    +--------+
| Flask App      | -> | OpenTelemetry| -> | Alloy| -> | Loki   | -> | Grafana|
+----------------+    +--------------+    +------+    +--------+    +--------+

```

-   **Flask App**: Generates logs.
-   **OpenTelemetry**: Collects and exports logs.
-   **Alloy**: Receives logs from OpenTelemetry.
-   **Loki**: Stores and indexes logs.
-   **Grafana**: Visualizes logs from Loki.