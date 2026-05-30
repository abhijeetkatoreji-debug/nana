# Nana

```
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: emailservice
  name: emailservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: emailservice
  strategy: {}
  template:
    metadata:
      labels:
        app: emailservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/emailservice:v8.8.0
        name: emailservice
        ports:
        - containerPort: 8080
        resources: {}
----

apiVersion: v1
kind: Service
metadata:
  labels:
    app: emailservice
  name: emailservice
spec:
  ports:
  - name: 8080-8080
    port: 8080
    protocol: TCP
    targetPort: 8080
  selector:
    app: emailservice
  type: ClusterIP
```
