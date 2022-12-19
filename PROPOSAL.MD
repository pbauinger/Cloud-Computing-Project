# Monitoring and Alerting for a Python Application running on Kubernetes

The objective of this project is to implement monitoring and alerting for a Kubernetes cluster consisting of a single node. On the node we will run a simple Python application, for storing animals. The application provides a REST-API. Over this API it should be possible to query, create, update and delete animals from a relational database. The API will return the data as JSON. As database we will use [MariaDB](https://mariadb.org). The system will use [Prometheus](https://prometheus.io/docs/introduction/overview/) to collect metrics of the node, the database and the Python application. For that we will modify the Python Application that it exposes metrics using https://github.com/prometheus/client_python. The metrics then can be pulled by Prometheus. We want to get at least the following metrics for the python application:
 - CPU usage
 - Memory usage
 - Network traffic
 - Total requests
 - Failed requests
 - Number of exceptions

For the node we want to get at least the following metrics:
 - CPU usage
 - Memory usage
 - Available storage

For the database we want to get the following metrics:
 - CPU usage
 - Memory usage
 - Network traffic

We will use [Grafana](https://grafana.com/docs/grafana/latest/introduction/) to visualize these metrics as graphs (since it supports querying for Prometheus, see [source](https://prometheus.io/docs/visualization/grafana/)).

For testing (and demonstration) we will first run the application only one a single pod. We will load test the application and therefore trigger alerts when it becomes unresponsive. We then increase the number of pods and check if we can handle more load.

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
is a package manager for Kubernetes. Helm works with Charts. Charts bundle all required resources to run a application. For most programs there are already existing Helm charts which can be easily installed. Doing the installation manually would be more work since applications usually consist of multiple services, configmaps, deployments and so on.

Install instructions: https://helm.sh/docs/intro/install/

### Prometheus
is an open-source system for monitoring and alerting. It collects metrics from monitored targets and stores them in a timeseries database. This is done with a pull-based approach, where the targets have to expose their metrics over a HTTP endpoint. The data can be queried with the provided query language PromQL.

We will install it with Helm and operate it directly in the cluster. Since we are only running on a single node, it wil run on the same node as the python application. 

The installation instructions can be found [here](https://prometheus-community.github.io/helm-charts/).


### Grafana
is an open source software that can be used to visualize metrics as graphs in multiple dashboards. It comes with Prometheus support by default and therefore we can use PromQL to build the dashboard visualizing our metrics. We will also run it directly in the cluster and also install it with Helm.

[Here](https://grafana.com/docs/agent/latest/operator/helm-getting-started/) is how to install Grafana w/ Helm.

### MariaDB
A open source relational database. Its a fork of MySQL. We will install it again with Helm https://artifacthub.io/packages/helm/bitnami/mariadb This Helm Chart already provides parameters for enabling Prometheus support (metrics.enabled) and enabling certain metrics (networkPolicy.metrics.enabled)


## Architecture
We will run the Python application, Prometheus and Grafana on a single node.

![Architecture](https://user-images.githubusercontent.com/16125084/208540887-16d47dd1-84db-4111-b805-5fa912761ff1.png)

