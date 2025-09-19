README
======


### How to create a boilerplate helm chart
```bash
helm create grafana-alloy-chart-v3
```


### How to make a dependency file (tgz)
* Steps:
  1. Git clone:
     ```bash
     git clone https://github.com/grafana/k8s-monitoring-helm.git
     ```
  2. Create a tgz file:
     ```
     helm package k8s-monitoring-helm/charts/k8s-monitoring
     ```
     - OUTPUT:
       - The `k8s-monitoring-3.5.1.tgz` file is created.


### How to add a dependency
* Steps:
  1. Copy tgz file to the charts directory:
     ```bash
     cp k8s-monitoring-3.5.1.tgz grafana-alloy-chart-v3/charts
     ```

  2. In Chart.yaml, add the followings:
     ```yaml
     dependencies:
       - name: k8s-monitoring           # must match the "name" in the dependency's Chart.yaml
         version: 3.5.1
         alias: grafana-k8s-monitoring  # optional; lets you refer to it by a different name in values.yaml
     ```


### Install
* Steps:
  1. Create a helm template preview file:
     ```bash
     helm template myapp charts -f values.yaml \
       --set-string 'grafana-k8-monitoring.destinations[0].basicAuth.password'="$GRAFANA_TOKEN" > post-rendering/base/preview.yaml
     ```

  2. Deploy:
     ```bash
     kubectl apply -f post-rendering/base/preview.yaml 
     ```

