# Nana

```yaml
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
        name: service
        ports:
        - containerPort: 8080
        env:
        - name: PORT
          value: "8080"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: emailservice
  name: emailservice
spec:
  type: ClusterIP
  selector:
    app: emailservice
  ports:
  - port: 5000
    protocol: TCP
    targetPort: 8080

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: recommendationservice
  name: recommendationservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: recommendationservice
  strategy: {}
  template:
    metadata:
      labels:
        app: recommendationservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/recommendationservice:v8.8.0
        name: service
        ports:
        - containerPort: 8080
        env:
        - name: PORT
          value: "8080"
        - name: PRODUCT_CATALOG_SERVICE_ADDR
          value: "productcatalogservice:3550"
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: recommendationservice
  name: recommendationservice
spec:
  type: ClusterIP
  selector:
    app: recommendationservice
  ports:
  - port: 8080
    protocol: TCP
    targetPort: 8080

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: productcatalogservice
  name: productcatalogservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: productcatalogservice
  strategy: {}
  template:
    metadata:
      labels:
        app: productcatalogservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/productcatalogservice:v8.8.0
        name: service
        ports:
        - containerPort: 3550
        env:
        - name: PORT
          value: "3550"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: productcatalogservice
  name: productcatalogservice
spec:
  type: ClusterIP
  selector:
    app: productcatalogservice
  ports:
  - port: 3550
    protocol: TCP
    targetPort: 3550

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: paymentservice
  name: paymentservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: paymentservice
  strategy: {}
  template:
    metadata:
      labels:
        app: paymentservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/paymentservice:v8.8.0
        name: service
        ports:
        - containerPort: 50051
        env:
        - name: PORT
          value: "50051"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: paymentservice
  name: paymentservice
spec:
  type: ClusterIP
  selector:
    app: paymentservice
  ports:
  - port: 50051
    protocol: TCP
    targetPort: 50051

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: currencyservice
  name: currencyservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: currencyservice
  strategy: {}
  template:
    metadata:
      labels:
        app: currencyservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/currencyservice:v8.8.0
        name: service
        ports:
        - containerPort: 7000
        env:
        - name: PORT
          value: "7000"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: currencyservice
  name: currencyservice
spec:
  type: ClusterIP
  selector:
    app: currencyservice
  ports:
  - port: 7000
    protocol: TCP
    targetPort: 7000

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: shippingservice
  name: shippingservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: shippingservice
  strategy: {}
  template:
    metadata:
      labels:
        app: shippingservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/shippingservice:v8.8.0
        name: service
        ports:
        - containerPort: 50051
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: shippingservice
  name: shippingservice
spec:
  type: ClusterIP
  selector:
    app: shippingservice
  ports:
  - port: 50051
    protocol: TCP
    targetPort: 50051

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: adservice
  name: adservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: adservice
  strategy: {}
  template:
    metadata:
      labels:
        app: adservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/adservice:v8.8.0
        name: service
        ports:
        - containerPort: 9555
        env:
        - name: PORT
          value: "9555"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: adservice
  name: adservice
spec:
  type: ClusterIP
  selector:
    app: adservice
  ports:
  - port: 9555
    protocol: TCP
    targetPort: 9555

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: cartservice
  name: cartservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: cartservice
  strategy: {}
  template:
    metadata:
      labels:
        app: cartservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/cartservice:v8.8.0
        name: service
        ports:
        - containerPort: 7070
        env:
        - name: PORT
          value: "7070"
        - name: RESDIS_ADDR
          value: "XXXX"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: cartservice
  name: cartservice
spec:
  type: ClusterIP
  selector:
    app: cartservice
  ports:
  - port: 7070
    protocol: TCP
    targetPort: 7070

----

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
        env:
        - name: PORT
          value: "8080"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: emailservice
  name: emailservice
spec:
  type: ClusterIP
  selector:
    app: emailservice
  ports:
  - port: 5000
    protocol: TCP
    targetPort: 8080

----

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
        env:
        - name: PORT
          value: "8080"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: emailservice
  name: emailservice
spec:
  type: ClusterIP
  selector:
    app: emailservice
  ports:
  - port: 5000
    protocol: TCP
    targetPort: 8080

----

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
        env:
        - name: PORT
          value: "8080"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: emailservice
  name: emailservice
spec:
  type: ClusterIP
  selector:
    app: emailservice
  ports:
  - port: 5000
    protocol: TCP
    targetPort: 8080

----

```
