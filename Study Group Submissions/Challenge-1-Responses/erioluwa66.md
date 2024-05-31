**Name**: Jumoke

**Email**: jumokeade210@gmail.com   


## Task 1: Deployment Configuration

**Objective:** Configure deployments for development and production applications using `nginx:latest` image, ensuring appropriate scheduling on labeled nodes.

**Development Application (`development-app.yaml`):**

```yaml
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
        - name: dev-app
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
          
      
