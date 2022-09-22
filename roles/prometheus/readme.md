# Query for CPU Usage Average:

```
 ceil(100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[1m])) * 100))
```

# Query for Mem Usage :
```
 100 * ((node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) /  node_memory_MemTotal_bytes)
 ceil(100 * ((node_memory_MemTotal_bytes - node_memory_MemAvailable_bytes) /  node_memory_MemTotal_bytes))
```

# Service Up Or Not:
```
 node_systemd_unit_state{instance="cart-dev-0", name ="cart.service", state="active"}
``` 
