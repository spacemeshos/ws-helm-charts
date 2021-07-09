# Add custom dashboard to Grafana

Helm Chart [sm-prom](https://github.com/spacemeshos/ws-helm-charts/tree/main/charts/sm-prom)
installs Grafana and custom dashboards can be added during this process.

To get dashboard as json file you may go to `Dashboard settings` in Grafana
dashboard, then click `JSON Model` and copy all json data.

[Main Dashboard](https://github.com/spacemeshos/ws-helm-charts/blob/main/charts/sm-prom/templates/grafana/main_dashboard.yaml)
can be used as an example. You should change spacemesh-main.json file name to
spacemesh-\<some\>.json and replace json data with your new dashboard. It's
important to note that you have to escape all chars that `gotemplate` will
interpet. For example `{{` have to be changed to ``{{`{{`}}``.
