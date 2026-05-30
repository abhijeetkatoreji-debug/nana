# nana

```
echo -n "username" | base64
echo -n "password" | base64

k create secret generic mongodb-secet  --from-literal=username=dXNlcm5hbWU= --from-literal=password=cGFzc3dvcmQ=
```

`k create deploy mongo-db --image=mongo --replicas=1 -oyaml --dry-run=client`
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
