**Name**: Jumoke

**Email**: jumokeade210@gmail.com

## Task 1: Deployment Configuration

**Objective:** Configure deployments for development and production applications using `nginx:latest` image, ensuring appropriate scheduling on labeled nodes.

**Development Application (`development-app.yaml`):**

````yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: dev-app
  template:
    metadata:
      labels:
        app: dev-app
    spec:
      containers:
        - name: app-container
          image: nginx:latest
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              - matchExpressions:
                  - key: environment
                    operator: In
                    values:
                      - development
````

**Production Application (`production-app.yaml`):**


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: production-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: prod-app
  template:
    metadata:
      labels:
        app: prod-app
    spec:
      containers:
        - name: app-container
          image: nginx:latest
      affinity:
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
              - matchExpressions:
                  - key: environment
                    operator: In
                    values:
                      - production


```

## Task 2: Log Inspection

After successfully deploying the applications, you need to inspect the logs of the three pods within the production environment.

```
kubectl logs -l app=prod-app
```

This command retrieves logs from all containers within the pods that match the label selector `app=prod-app`. It helps you monitor and troubleshoot the production environment effectively.

By following these steps, you ensure that the development and production applications are appropriately configured and that you can access their logs for maintenance and debugging purposes.

 kubectl logs -l  app=prod-app
2024/06/01 01:25:55 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/06/01 01:25:55 [notice] 1#1: start worker processes
2024/06/01 01:25:55 [notice] 1#1: start worker process 34
2024/06/01 01:25:55 [notice] 1#1: start worker process 35
2024/06/01 01:25:55 [notice] 1#1: start worker process 36
2024/06/01 01:25:56 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/06/01 01:25:56 [notice] 1#1: start worker processes
2024/06/01 01:25:56 [notice] 1#1: start worker process 30
2024/06/01 01:25:56 [notice] 1#1: start worker process 37
2024/06/01 01:25:56 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
