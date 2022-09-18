# Query for CPU Usage Average
## ceil(100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100))

