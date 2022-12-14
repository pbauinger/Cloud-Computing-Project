# Monitoring and Alerting for a Python Application running on Kubernetes

The objective of this project is to implement monitoring and alerting for a Kubernetes cluster consisting of a single node running a simple Python application. The system will use Prometheus to collect metrics of the node and the Python application. For that we will modify the Python Application that it exposes metrics which then can be pulled by Prometheus. We want to get at least the following metrics for the python application:
 - Total requests
 - Failed requests
 - Request success rate
 - Number of exceptions

For the node we want to get at least the following metrics:
 - CPU usage
 - Memory usage
 - Available storage

We will use Grafana to visualize these metrics as graphs. 

The python service should provide a REST API. At first we will run the application only one a single pod. We will load test the application and therefore trigger alerts when it becomes unresponsive. We then increase the number of pods and check if we can handle more load.
