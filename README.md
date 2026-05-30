# nana

```
echo -n "username" | base64
echo -n "password" | base64

k create secret generic mongodb-secet  --from-literal=username=dXNlcm5hbWU= --from-literal=password=cGFzc3dvcmQ=
```

```https://hub.docker.com/_/mongo```

<img width="274" height="69" alt="image" src="https://github.com/user-attachments/assets/423dab38-77c2-4838-94f2-50c1c4301017" />
<img width="722" height="223" alt="image" src="https://github.com/user-attachments/assets/aa1891e2-27d8-471c-96d4-481b0a5cb7b2" />



```shell
k create deploy mongo-db --image=mongo --replicas=1 -oyaml --dry-run=client
```
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: mongo-db
  name: mongo-db
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo-db
  strategy: {}
  template:
    metadata:
      labels:
        app: mongo-db
    spec:
      containers:
      - image: mongo
        name: mongo
        ports:
          - containerPort: 27017
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          valueFrom:
            secretKeyRef:
              key: username
              name: mongodb-secet
        - name: MONGO_INITDB_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              key: password
              name: mongodb-secet
        resources: {}
status: {}
```


k expose deployment mongo-db --port=27017 --target-port=27017 --protocol='TCP'

----
config

```https://hub.docker.com/_/mongo-express```

```shell
$ docker run --network some-network -e ME_CONFIG_MONGODB_SERVER=some-mongo -p 8081:8081 mongo-express
```

<img width="1219" height="876" alt="image" src="https://github.com/user-attachments/assets/160e63ec-30ca-4e35-9b4b-e01779f86352" />

```shell
k create deploy mongo-express --image=mongo --replicas=1 -oyaml --dry-run=client
```

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: mongo-express
  name: mongo-express
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mongo-express
  strategy: {}
  template:
    metadata:
      labels:
        app: mongo-express
    spec:
      containers:
      - image: mongo-express
        name: mongo-express
        ports:
        - containerPort: 8081
        env:
        - name: ME_CONFIG_MONGODB_ADMINUSERNAME
          valueFrom:
            secretKeyRef:
              key: username
              name: mongodb-secet

        - name: ME_CONFIG_MONGODB_ADMINPASSWORD
          valueFrom:
            secretKeyRef:
              key: password
              name: mongodb-secet
        - name: ME_CONFIG_MONGODB_SERVER
          valueFrom:
            configMapKeyRef:
              key: database_url
              name: mongodb-configmap
        resources: {}
status: {}
```

## config-map (mongo-configmap)

```
k create cm mongodb-configmap --from-literal=database_url=mongodb-service
```
