# Monitoring and Alerting for a Python Application running on Kubernetes

The objective of this project is to implement monitoring and alerting for a Kubernetes cluster consisting of a single node running a simple Python application. The system will use [Prometheus](https://prometheus.io/docs/introduction/overview/) to collect metrics of the node and the Python application. For that we will modify the Python Application that it exposes metrics using https://github.com/prometheus/client_python. The metrics then can be pulled by Prometheus. We want to get at least the following metrics for the python application:
 - Total requests
 - Failed requests
 - Number of exceptions

For the node we want to get at least the following metrics:
 - CPU usage
 - Memory usage
 - Available storage

We will use [Grafana](https://grafana.com/docs/grafana/latest/introduction/) to visualize these metrics as graphs (since it supports querying for Prometheus, see [source](https://prometheus.io/docs/visualization/grafana/)).

The python service should provide a REST API. At first we will run the application only one a single pod. We will load test the application and therefore trigger alerts when it becomes unresponsive. We then increase the number of pods and check if we can handle more load.

We will use [Helm](https://helm.sh/docs/) to install Prometheus and Grafana.

## Work distribution:
| Topic        | Philipp   | Nico       |
|--------------|-----------|------------|
| Documentation (Research) |      |   X   |
| Documentation (Tutorial: Instructions & Reproducibility) |   X   |      |
| Helm Setup   |   X   |      |
| Grafana & Prometheus Setup |   X   |   X   |
| Script.py (including Prometheus-Client Library) |   X   |   X   |
| Try Local hosting |   X   |   X   |
| Setup Cloud hosting (gCloud) |     |   X   |


## Software
### Helm
is the package manager for Kubernetes. It's [requirements](https://helm.sh/docs/intro/quickstart/#prerequisites) are:
- a kubernetes cluster
- security configurations (if any)
- [local configured copy of kubectl]

Here you can find the [installation steps](https://helm.sh/docs/intro/install/).

### Prometheus
is an open-source toolkit for system monitoring and alerting. It collects metrics from monitored targets by collecting metrics HTTP endpoints on them.

The installation instructions can be found [here](https://prometheus-community.github.io/helm-charts/).



### Grafana
is an open-source software that enables you to query, visualize, alert on, and explore metrics, logs, and traces wherever they are stored.

[Here](https://grafana.com/docs/agent/latest/operator/helm-getting-started/) is how to install Grafana w/ Helm.

# Architecture
![Architecture](/Architecture.drawio.png")
