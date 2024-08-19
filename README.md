# Monitoring Setup

This repo contains helm and kubernetes definitions for bringing up JFrog Artifactory and monitoring stack. The goal is logs and metric to be collected from Jfrog and Kubernetes and forwared to the monitoring stack via OpenTelemetry Collector.

The monitoring stack used is Prometheus/Loki conected to Grafana.

The forwarding of the JFrog Artifactory is achived by creating sidecard pod with shared log files volume. We have used file `receiver` and loki `exporter` to forward the logs to grafana.

For Kubernetes setup, it is used OpenTelemetry Collector (run as daemon)using kubeletstats `receiver` and `prometheus exporter`.


## Deployments

Github Action makes install of the following:
 - Prometheus 
 - Grafana
 - Loki
 - JFrog

## Manual steps after Deployment

### Steps for Grafana
 - Obtain default password running the following command: `kubectl get secret --namespace yaro-task grafana-yaro -o jsonpath="{.data.admin-password}" | base64 -d ; echo`
 - Create data source for Prometheus using `Prometheus server URL: http://prometheus-yaro-server.yaro-task.svc.cluster.local`
 - Create data source for Loki using `URL: http://loki-yaro-gateway.yaro-task.svc.cluster.local/`
