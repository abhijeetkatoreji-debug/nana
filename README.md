# Nana
https://github.com/GoogleCloudPlatform/microservices-demo/tree/main/release

Image version: v0.10.5
<img width="1907" height="902" alt="image" src="https://github.com/user-attachments/assets/93d975e7-02aa-4801-b345-5b5c7607c376" />

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
      - image: gcr.io/google-samples/microservices-demo/emailservice:v0.10.5
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
      - image: gcr.io/google-samples/microservices-demo/recommendationservice:v0.10.5
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
      - image: gcr.io/google-samples/microservices-demo/productcatalogservice:v0.10.5
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
      - image: gcr.io/google-samples/microservices-demo/paymentservice:v0.10.5
        name: service
        ports:
        - containerPort: 50051
        env:
        - name: PORT
          value: "50051"
        - name: DISABLE_PROFILER
          value: "1"
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
      - image: gcr.io/google-samples/microservices-demo/currencyservice:v0.10.5
        name: service
        ports:
        - containerPort: 7000
        env:
        - name: PORT
          value: "7000"
        - name: DISABLE_PROFILER
          value: "1"
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
      - image: gcr.io/google-samples/microservices-demo/shippingservice:v0.10.5
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
      - image: gcr.io/google-samples/microservices-demo/adservice:v0.10.5
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
      - image: gcr.io/google-samples/microservices-demo/cartservice:v0.10.5
        name: service
        ports:
        - containerPort: 7070
        env:
        - name: PORT
          value: "7070"
        - name: RESDIS_ADDR
          value: "redis-cart:6379"
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
    app: redis-cart
  name: redis-cart
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis-cart
  strategy: {}
  template:
    metadata:
      labels:
        app: redis-cart
    spec:
      containers:
      - image: redis:alpine
        name: redis-cart
        ports:
        - containerPort: 6379
        volumeMounts:
        - name: redis-data
          mountPath: /data
      volume:
      - name: redis-data
        emptyDir: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: redis-cart
  name: redis-cart
spec:
  type: ClusterIP
  selector:
    app: redis-cart
  ports:
  - port: 6379
    protocol: TCP
    targetPort: 6379

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: checkoutservice
  name: checkoutservice
spec:
  replicas: 1
  selector:
    matchLabels:
      app: checkoutservice
  strategy: {}
  template:
    metadata:
      labels:
        app: checkoutservice
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/checkoutservice:v0.10.5
        name: service
        ports:
        - containerPort: 5050
        env:
        - name: PORT
          value: "5050"
        - name: PRODUCT_CATALOG_SERVICE_ADDR
          value: "productcatalogservice:3550"
        - name: SHIPPING_SERVICE_ADDR
          value: "shippingservuce:50051"
        - name: PAYMENT_SERVICE_ADDR
          value: "paymentservice:50051"
        - name: EMAIL_SERVICE_ADDR
          value: "emailservice:5000"
        - name: CURRENCY_SERVICE_ADDR
          value: "currencyservice:7070"
        - name: CART_SERVICE_ADDR
          value: "cartservice:7070"
        resources: {}
----
apiVersion: v1
kind: Service
metadata:
  labels:
    app: checkoutservice
  name: checkoutservice
spec:
  type: ClusterIP
  selector:
    app: checkoutservice
  ports:
  - port: 5050
    protocol: TCP
    targetPort: 5050

----

apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: frontend
  name: frontend
spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend
  strategy: {}
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
      - image: gcr.io/google-samples/microservices-demo/frontend:v0.10.5
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
    app: frontend
  name: frontend
spec:
  type: ClusterIP
  selector:
    app: frontend
  ports:
  - port: 8080
    protocol: TCP
    targetPort: 8080

----

```
