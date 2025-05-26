# Monitoring and Logging in DevOps

## Grafana
### Building a Multi-Panel Dashboard in Grafana
#### Prerequisite 
- Setup prometheus with Node Exporter

#### Configure Prometheus as data source in Grafana
1. Login into Grafana (here http://localhost:3000)
**Note**: Please ensure that Prometheus and Node Exporter are installed and running before starting the Grafana server.
2. In the Grafana dashboard, select **Connections** and then **Data sources** from the menu on the left side. Then, select **Add data source**

    [ **Connections** -> **Data sources** ->  **Add data source** ]
3. Choose **Prometheus**, data source from the list
4. Give the name of the connection.Here it is **connection-prometheus**   
5. **Connection** -> Give Prometheus Server URL[**http://localhost:9090**]
6. **Save & Exit**

#### Create a dashboard in Grafana for visualizing Prometheus metrics
1. **Dashboards** -> **Create Dashboard**
2. Choose **Import dashboard**
3. Go to **Find and import dashboard for common applications**
4. Enter **1860** there and then click **Load**
5. Click **Select a Prometheus data source** under **Prometheus**
6. Select **connection-prometheus**  and then click **Import**
7. We can see the Multiple panels are created under the dashboard, showing different resource metrics 

### Creating a Grafana Dashboard Using PromQL Queries to Visualize Specific Application Metrics
1. Choose **Dashboards** -> **+ Add visualization**
2. **New** -> **New dashboard**
3. Select **connection-prometheus** from the data source list
4. Select **Time Series** as the panel type and change the **Title** of the panel to **CPU Usage** under Panel options
5. **Query** -> **Code** (Button)
6. Enter the following query and click **Run queries** to execute it:
    - `100 - (avg by(instance)(rate(node_cpu_seconds_total{mode='idle'}[5m]))* 100)`
7. Click **Apply** to add the graph to the page.
8. Press **Save**[icon] and give the Dashboard Name and **Save**
9. **Add** -> **Visualization** for adding new graph to the dashboard.Then save the dashboard again.